# Entity Search & Co-Occurrence

## Introduction <a id="EntityCooccurrenceSearch-Introduction"></a>

This feature generalizes the ability to:

* given one or more kind instances \(i.e., entities\) \(and their surface forms\) and an optional graph scope \(kind, field, instance\), what are the \(co\)occurrences \(kind, field, instance, locations\)?

For example, the City of New York entity might be represented in the CKG as:

* kind:City \# type of thing
* id:992 \# instance
* name: "New York City" \# canonical form
* ...

But there are many surface forms \(i.e., synonyms\) for this instance:  Big Apple, New Amsterdam, New York City, "NY, NY", NY, NYC, City of New York, "New York, New York"

It should be possible, given this kind instance and its surface forms, to find references of one of the surface forms in the CKG.  Typically this will be **scoped** to a particular Kind/Field \(e.g., k:Document.text\) or even a specific instance \(e.g., "The Great Gatsby" book\).

It should also be possible to find **co-occurrences** of multiple such entities \(e.g., City: New York and Author: F. Scott Fitzgerald\).

### Surface Form Usage <a id="EntityCooccurrenceSearch-SurfaceFormUsage"></a>

To support surface forms users must define a surface form kind with the following schema.

```
type SurfaceForm {
  # required
  id: ID! # surface form id (e.g., "Big Apple@en-us"); language code can be omitted
  # optional/inferred
  name: String # surface form (e.g., "Big Apple")
  lang: String # language code ISO 639-2 and ISO 3166-2 (e.g., en-us)
}
```

A link should then be established between an instance of an entity and its surface form\(s\) \(a one to many relationship\) via a 'hasSurfaceForm' relation. 

### Example:

```
mutation
{
    addLink(input:{
        fromKindName: "Actor"
        fromInstanceId: "A1" # e.g. refer to "Harrison Ford"
        toKindName: "SurfaceForm"
        toInstanceId: "SF1" # e.g. refer to "Harrison Ford"
        relationName: "hasSurfaceForm"
  })
}
```

The link allows the Maana Q platform to automatically infer the surface forms when performing an entity search \(See Query Behavior below\).

## Entity Search <a id="EntityCooccurrenceSearch-EntitySearch"></a>

### GraphQL <a id="EntityCooccurrenceSearch-GraphQL"></a>

```
input EntitySurfaceFormsInput {
  # The entity (i.e., a Kind instance)
  kindId: ID! # kind id of the entity, e.g. id of City kind
  instanceId: [ID!] # instance id of the entity kind, e.g. 992 (New York City)
  # Various textual representations
  surfaceForms: [String!] # may be null, in which case all known surface forms will be used
}
 
input EntitySearchInput {
  # what to search for
  entitySurfaceForms: [EntitySurfaceFormsInput!]!
 
  # where to search
  scopeKindId: ID! # kind id to be search on
  scopeFieldId: ID! # field id on the kind to be search on
  # optionally a specific instances
  scopeInstanceId: [ID!]
}
 
 
type EntityOccurrences {
  # The entity (i.e., a Kind instance)
  kindId: ID!
  instanceID: ID!
 
  # Offsets where one of its surface forms was found
  locations: [Int!]!
}
 
type EntitySearchResult {
  # Context (i.e., where found)
  scopeKindId: ID!
  scopeFieldId: ID!
  scopeInstanceId: ID!
 
  # Cooccurring instances and their locations (i.e., what found)
  cooccurrences: [EntityOccurrences!]!
}
type EntitySearchActionResult {
  results: [EntitySearchResult!]
  token: String
}
 
 
type Query {
  entitySearch(input: EntitySearchInput!): [EntitySearchResult!]
  entitySearchResult(
    resultKey: String!
    token: String
    take: Int
  ): EntitySearchActionResult!
}
 
type Mutation {
  entitySearchAction(input: EntitySearchInput!, resultKey: String): BotAction!
}
```

### Query Behavior \(EntitySurfaceFormsInput\) <a id="EntityCooccurrenceSearch-QueryBehavior(EntitySurfaceFormsInput)"></a>

* If only a kind id is specified, all entities \(using their defined surface forms\*\) are search for.
  * Example:  Use all defined surface forms associated with the kind \(an entity\) with id "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"

```
{
  entitySearch(input:{
    scopeKindId: "88dd0992-b5e3-4272-b0f4-763d0d975f8e"
    scopeFieldId: "4f24e664-d7e0-45bd-8437-5f6c7c3aa767"
    entitySurfaceForms: [
      {
        kindId: "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"
      }
    ]
  }) {
    scopeKindId
    scopeFieldId
    scopeInstanceId
    cooccurrences {
      kindId
      instanceId
      locations
    }
  }
}
```



* If a kind id and instance id\(s\) are provided, then only those entities are searched for \(using their defined surface forms\*\).
  * Example:  Use all defined surface forms associated with the specified instances "A1" and "A2" of the kind \(an entity\) with id "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"

```
{
  entitySearch(input:{
    scopeKindId: "88dd0992-b5e3-4272-b0f4-763d0d975f8e"
    scopeFieldId: "4f24e664-d7e0-45bd-8437-5f6c7c3aa767"
    entitySurfaceForms: [
      {
        kindId: "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"
        instanceId:["A1", "A2"]
      }
    ]
  }) {
    scopeKindId
    scopeFieldId
    scopeInstanceId
    cooccurrences {
      kindId
      instanceId
      locations
    }
  }
}
```

* Explicit surface forms may only be used when providing only one instance id. The instance id must belong to an existing entity.
* * Example:  Use all specified surface forms \["HF", "H. Ford"\] to search on the specific instance "A1" of the kind \(an entity\) with id "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"

```
{
  entitySearch(input:{
    scopeKindId: "88dd0992-b5e3-4272-b0f4-763d0d975f8e"
    scopeFieldId: "4f24e664-d7e0-45bd-8437-5f6c7c3aa767"
    entitySurfaceForms: [
      {
        kindId: "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"
        instanceId:["A1"]
        surfaceForms: ["HF", "H. Ford"]
      }
    ]
  }) {
    scopeKindId
    scopeFieldId
    scopeInstanceId
    cooccurrences {
      kindId
      instanceId
      locations
    }
  }
}
```

{% hint style="info" %}
NOTE: A kind defining surface forms must be pre-defined with instances in kinds for both entities and surfaces forms being linked by a "hasSurfaceForm" relationship.
{% endhint %}

### Example: Corpus and Entities

```
# Document / Corpus kind
const movieNews = [
  { id: "MN01", bodyText: "George Lucas directed Star Wars (1977). Star Wars stars Harrison Ford, Mark Hamill, and Carrie Fisher." },
  { id: "MN02", bodyText: "H. Ford appeared at the Star Wars reunion with director Lucas" },
  ...
]
 
 
# Entity kind 1
const actors = [
  { id: "A1", fullname: "Harrison Ford" },
  { id: "A2", fullname: "Carrie Fisher" },
  { id: "A3", fullname: "Jacky Chan" },
  ...
]
 
# Entity kind 2
const movies = [
  { id: "M1", fullname: "Star Wars" },
  { id: "M2", fullname: "Wishful Drinking" },
  ...
]
 
# Entity kind 3
const directors = [
  { id: "D1", fullname: "Steven Spielberg" },
  { id: "D2", fullname: "George Lucas" },
  ...
]
```

### Query

**Assumptions:**

* Entity kind id of "Actor": "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed"
* Entity kind id of "Movie": "15cb20fb-63ca-472e-8c6e-0d7c0e873039"
* Entity kind id of "Director": "8642d9aa-be4b-498b-8d86-fe7b94af11a9"
* Corpus kind id of "MovieNews": "a96afffe-0b73-425e-b9aa-3531ec8c3d0c"
* Field id of the field containing text in the MovieNews kind is: "89d1e030-25be-412b-81e9-54588fa17042"

```
const entitySurfaceForms = [
  { kindId:"6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed", instanceId: "A1", surfaceForms: ["Harrison Ford", "H. Ford"]},
  { kindId:"15cb20fb-63ca-472e-8c6e-0d7c0e873039", instanceId: "M1", surfaceForms: ["Star Wars (1977)", "Star Wars"]},
  { kindId:"8642d9aa-be4b-498b-8d86-fe7b94af11a9", instanceId: "D2", surfaceForms: ["George Lucas", "Lucas"]}
]
 
const entitySearch = {
  entitySurfaceForms,
  scopeKindId: "MovieNews",
  scopeFieldId: "bodyText"
}
 
 
const entityCooccurrences = kindDb.entitySearch(entitySearch)
```

### Results <a id="EntityCooccurrenceSearch-Results"></a>

```
[{
  "scopeKindId": "a96afffe-0b73-425e-b9aa-3531ec8c3d0c", # id of "MovieNews" kind
  "scopeFieldId": "89d1e030-25be-412b-81e9-54588fa17042", # field id of "bodyText" of "MovieNews" kind
  "scopeInstanceId": "MN01",
  "cooccurrences": [
    {"kindId": "8642d9aa-be4b-498b-8d86-fe7b94af11a9", "instanceId": "A1",  "locations": [0]},    # for "Director"
    {"kindId": "15cb20fb-63ca-472e-8c6e-0d7c0e873039", "instanceId": "M1",  "locations": [3, 6]}, # for "Movie"
    {"kindId": "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed", "instanceId": "D2",  "locations": [9]},    # for "Actor"
  ]
},{
  "scopeKindId": "a96afffe-0b73-425e-b9aa-3531ec8c3d0c", # id of "MovieNews" kind
  "scopeFieldId": "89d1e030-25be-412b-81e9-54588fa17042", # field id of "bodyText" of "MovieNews" kind
  "scopeInstanceId": "MN02",
  "cooccurrences": [
    {"kindId": "8642d9aa-be4b-498b-8d86-fe7b94af11a9", "instanceId": "A1",  "locations": [0]},
    {"kindId": "15cb20fb-63ca-472e-8c6e-0d7c0e873039", "instanceId": "M1",  "locations": [5]},
    {"kindId": "6c2a72f4-df82-42d3-9a67-cd7d9a5a99ed", "instanceId": "D2",  "locations": [10]},
 
  ]
}]
```

## How To setup the above example? <a id="EntityCooccurrenceSearch-HowTosetuptheaboveexample?"></a>

```
# Here is the model.gql file:
type MovieNews {
  id: ID!
  bodyText: String!
}
 
type SurfaceForm {
  id: ID!
  name: String!
}
 
type Actor {
  id: ID!
  fullname: String!
}
 
type Movie {
  id: ID!
  fullname: String!
}
 
type Director {
  id: ID!
  fullname: String!
}
```

### Given the above model, add some instances to kinds using these mutations: <a id="EntityCooccurrenceSearch-Giventheabovemodel,addsomeinstancestokindsusingthesemutations:"></a>

```
# Documents or Corpus
mutation addMovieNewss {
  addMovieNewss(
    input: [
      {
        id: "MN01"
        bodyText: "George Lucas directed Star Wars (1977). Star Wars stars Harrison Ford, Mark Hamill, and Carrie Fisher."
      }
      {
        id: "MN02"
        bodyText: "H. Ford appeared at the Star Wars reunion with director Lucas"
      }
    ]
  )
}
 
# Surface forms are like synonyms
mutation addSurfaceForms {
  addSurfaceForms(
    input: [
      { id: "SF1", name: "Harrison Ford" }
      { id: "SF2", name: "H. Ford" }
      { id: "SF3", name: "Star Wars (1977)" }
      { id: "SF4", name: "Star Wars" }
      { id: "SF5", name: "George Lucas" }
      { id: "SF6", name: "Lucas" }
    ]
  )
}
 
# Entity
mutation addActors {
  addActors(
    input: [
      { id: "A1", fullname: "Harrison Ford" }
      { id: "A2", fullname: "Carrie Fisher" }
      { id: "A3", fullname: "Jacky Chan" }
    ]
  )
}
 
# Entity
mutation addMovies {
  addMovies(
    input: [
      { id: "M1", fullname: "Star Wars" }
      { id: "M2", fullname: "Wishful Drinking" }
    ]
  )
}
 
# Entity
mutation addDirectors {
  addDirectors(
    input: [
      { id: "D1", fullname: "Steven Spielberg" }
      { id: "D2", fullname: "George Lucas" }
    ]
  )
}
```

### Add links from each entity kind to SurfaceForm kind: <a id="EntityCooccurrenceSearch-AddlinksfromeachentitykindtoSurfaceFormkind:"></a>

In this example, we will set up these links:

1. From Actor's A1 to SurfaceForm SF1
2. From Actor's A1 to SurfaceForm SF2
3. From Movie's M1 to SurfaceForm SF3
4. From Movie's M1 to SurfaceForm SF4
5. From Director's D2 to SurfaceForm SF5
6. From Director's D2 to SurfaceForm SF6

```
# Here is the addLink mutation you can use:
mutation addLink(
  $fromKindId: ID!
  $fromInstanceId: ID!
  $toKindId: ID!
  $toInstanceId: ID!
) {
  addLink(
    input: {
      fromKindId: $fromKindId # e.g. id of the “Actor” entity kind
      fromInstanceId: $fromInstanceId  # e.g. "A1"
      toKindId: $toKindId # id of the "SurfaceForm" kind
      toInstanceId: $toInstanceId # e.g. "SF1"
      relationName: "hasSurfaceForm" # the relation
    }
  )
}
```

### The Workspace should look like this with links from each Entity kinds to SurfaceForm kind: <a id="EntityCooccurrenceSearch-TheWorkspaceshouldlooklikethiswithlinksfromeachEntitykindstoSurfaceFormkind:"></a>

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/f5.png)

### When the above setup is done, use one of the following: <a id="EntityCooccurrenceSearch-Whentheabovesetupisdone,useoneofthefollowing:"></a>

1. Run "EntitySearch" query
2. Run "EntitySearchAction" mutation

#### Run "EntitySearch" on given entities \(using all their defined surface forms\): <a id="EntityCooccurrenceSearch-Run&quot;EntitySearch&quot;ongivenentities(usingalltheirdefinedsurfaceforms):"></a>

```
# Here is the query:
query entitySearch_allEntities(
  $corpusId: ID!
  $corpusTextId: ID!
  $actorId: ID!
  $movieId: ID!
  $directorId: ID!
) {
  entitySearch(
    input: {
      scopeKindId: $corpusId # id of the corpus kind
      scopeFieldId: $corpusTextId # id of the field in the corpus kind
      entitySurfaceForms: [
        {
          # NOTE: all entities (using their defined surface forms) are search for
          # NOTE: instanceId and surfaceForms are optional
          kindId: $actorId # id of Actor Entity kind
        }
        {
          kindId: $movieId # id of Movie Entity kind
        }
        {
          kindId: $directorId # id of Director Entity kind
        }
      ]
    }
  ) {
    ...entitySearchResultInfo
  }
}
 
 
fragment entitySearchResultInfo on EntitySearchResult {
  scopeKindId
  scopeFieldId
  scopeInstanceId
  cooccurrences {
    kindId
    instanceId
    locations
  }
}
```

**Ran the above "EntitySearch" query, the result is:**

```
# Here is the result:
{
  "data": {
    "entitySearch": [
      {
        "scopeKindId": "ae582511-fdec-4429-bdef-01ed918c3353",
        "scopeFieldId": "b5163cd1-b3b6-45aa-a1d7-280e2d1b7244",
        "scopeInstanceId": "MN01",
        "cooccurrences": [
          {
            "kindId": "eb5572f3-850a-4d13-a73b-13a190e346ef",
            "instanceId": "A1",
            "locations": [
              9
            ]
          },
          {
            "kindId": "15cb20fb-63ca-472e-8c6e-0d7c0e873039",
            "instanceId": "M1",
            "locations": [
              3,
              6
            ]
          },
          {
            "kindId": "8642d9aa-be4b-498b-8d86-fe7b94af11a9",
            "instanceId": "D2",
            "locations": [
              0
            ]
          }
        ]
      },
      {
        "scopeKindId": "ae582511-fdec-4429-bdef-01ed918c3353",
        "scopeFieldId": "b5163cd1-b3b6-45aa-a1d7-280e2d1b7244",
        "scopeInstanceId": "MN02",
        "cooccurrences": [
          {
            "kindId": "8642d9aa-be4b-498b-8d86-fe7b94af11a9",
            "instanceId": "D2",
            "locations": [
              10
            ]
          },
          {
            "kindId": "15cb20fb-63ca-472e-8c6e-0d7c0e873039",
            "instanceId": "M1",
            "locations": [
              5
            ]
          },
          {
            "kindId": "eb5572f3-850a-4d13-a73b-13a190e346ef",
            "instanceId": "A1",
            "locations": [
              0
            ]
          }
        ]
      }
    ]
  }
}
```

#### Run "EntitySearchAction" mutation to create a bot: <a id="EntityCooccurrenceSearch-Run&quot;EntitySearchAction&quot;mutationtocreateabot:"></a>

```
mutation addESAction {
  entitySearchAction(
    resultKey: "resultA" # choose a unique string for resultKey
    input: {
      scopeKindId: "ae582511-fdec-4429-bdef-01ed918c3353"  # refer to "MovieNews"
      scopeFieldId: "b5163cd1-b3b6-45aa-a1d7-280e2d1b7244" # refer to "bodyText" in "MovieNews"
      entitySurfaceForms: [
        { kindId: "eb5572f3-850a-4d13-a73b-13a190e346ef" } # refer to "Actor"
        { kindId: "15cb20fb-63ca-472e-8c6e-0d7c0e873039" } # refer to "Movie"
        { kindId: "8642d9aa-be4b-498b-8d86-fe7b94af11a9" } # refer to "Director"
      ]
    }
  ) {
    ...botActionInfo
  }
}
 
fragment botActionInfo on BotAction {
  id
  name
  created
  lastUpdated
  status
  progress
  errors
}
```

**The bot id is returned from the above mutation:**

```
{
  "data": {
    "entitySearchAction": {
      "id": "c9bda58f-5924-447e-805b-d5939f1f658e",
      "name": "Entitiy Search, result key: resultA",
      "created": "2019-02-13T02:06:28.001Z",
      "lastUpdated": "2019-02-13T02:06:28.001Z",
      "status": "IN_PROGRESS",
      "progress": null,
      "errors": null
    }
  }
}
```

**When the bot completes, run a query to get the entity search result:**

```
query getESBot_byId($id: ID!) {
  botAction(id: $id) {
    ...botActionInfo
  }
}
 
fragment botActionInfo on BotAction {
  id
  name
  created
  lastUpdated
  status
  progress
  errors
}
```

**The result of "botAction" is:**

```
{
  "data": {
    "botAction": {
      "id": "c9bda58f-5924-447e-805b-d5939f1f658e",
      "name": "Entitiy Search, result key: resultA",
      "created": "2019-02-13T02:06:28.001Z",
      "lastUpdated": "2019-02-14T00:28:39.756Z",
      "status": "COMPLETE",
      "progress": 100,
      "errors": []
    }
  }
}
```

