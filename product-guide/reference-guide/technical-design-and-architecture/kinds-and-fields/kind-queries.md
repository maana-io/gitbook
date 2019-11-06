# Kind Queries

## Queries <a id="KindQueries-Queries"></a>

KindDB provides schema for Kind, Field, Instance, InstanceSet, FieldValue, etc. and CRUD queries/mutations/subscriptions.

What is missing, however, is a way to query/filter instances of a particular Kind.  This is not provided by the GraphQL standard.

As a motivating example, consider the familiar movies domain schema:

```
type Movie {
  id: ID!
  name: String! # e.g., "Cold Sweat"
  releaseYear: Int
}
 
 
type MovieGenre {
  id: ID!
  name: String! # e.g., "action"
  movieId: ID!
}
 
 
type Actor {
  id: ID!
  name: String! # e.g., "Charles Bronson"
}
 
 
type MovieActor {
  id: ID!
  movieId: ID!
  movie: Movie!
  actorId: ID!
  actor: Actor!
}
```

Consider the following additions to KindDB schema \(sketch\):

```
# Arbitrary filters applied to field values
type FieldFilter {
  fieldId: ID!
  op: String!
  value: FieldValueInput
}
 
# Query tree
type KindQuery {
  # projected kind
  kindId: ID!
  # filters (where)
  fieldFilters: [FieldFilter]
  # conjunction (where)
  and: [KindQuery]
  # disjunction (where)
  or: [KindQuery]
  # join (if conjunction or disjunction)
  fromFieldId: ID
  toFieldId: ID
}
```

And a new root query:

```
query(tenantId: ID!, input: KindQuery): InstanceSet
```

Consider the following exploration/query cases:

#### Movies with a specific release year \(i.e., simple value filter\)

```
const query = {
  kindId: 'Movie', // should be id, obviously
  filters: [{
    fieldId: 'releaseYear', // shouls be id, obviously
    op: '=',
    value: {INT: '1977'}
  }]
}
```

#### Movies released in a decade \(i.e., value range filter\)

```
const query = {
  kindId: 'Movie',
  filters: [{
    fieldId: 'releaseyear',
    op: '>',
    value: {INT: '1969'}
  },{
    fieldId: 'releaseyear',
    op: '<',
    value: {INT: '1980'}
  }]
}
```

#### Movies with a specific genre \(i.e., simple value filter through join\)

```
const query = {
  kindId: 'Movie',
  and:[{
    kindId: 'MovieGenre',
    fromFieldId: 'id',
    toFieldId: 'movieId'
    filters: [{
      fieldId: 'name',
      op: '=',
      value: {STRING: 'action'}
    }]
  }]
}
```

#### Movies with a specific actor \(i.e., simple value filter through join\)

```
const query = {
  kindId: 'Movie',
  and:[{
    kindId: 'MovieActor',
    fromFieldId: 'id',
    toFieldId: 'movieId',
    and: [{
      kindId: 'Actor',
      fromFieldId: 'actorId',
      toFieldId: 'id',
      filters: [{
        fieldId: 'name',
        op: '=',
        value: {STRING: 'Charles Bronson'}
      }]
    }]
  }]
}
```

#### Combination \(e.g., 1970s action movies with Charles Bronson\)

```
const query = {
  kindId: 'Movie',
  filters: [{
    fieldId: 'releaseYear',
    op: '>',
    value: {INT: '1969'}
  },{
    fieldId: 'releaseYear',
    op: '<',
    value: {INT: '1980'}
  }],
  and:[{
    kindId: 'MovieGenre',
    fromFieldId: 'id',
    toFieldId: 'movieId',
    filters: [{
      fieldId: 'name',
      op: '=',
      value: {STRING: 'action'}
    }]
  },{
    kindId: 'MovieActors',
    fromFieldId: 'id',
    toFieldId: 'movieId',
    and: [{
      kindId: 'Actor',
      fromFieldId: 'actorId',
      toFieldId: 'id',
      filters: [{
        fieldId: 'name',
        op: '=',
        value: {STRING: 'Charles Bronson'}
      }]   
    }]
  }]
}
```

#### Actor Co-occurrence in Genre

The following query fetches actors that co-occur in action moves with Harrison ford, excluding Harrison Ford from the resulting list.

```
const query = {
  kindId: 'Actor',
  filters: [{
    fieldId: 'name',
    op: '!=',
    value: {STRING: 'Harrison Ford'}
  }],
  and:[{
    kindId: 'MovieActor',
    fromFieldId: 'id',
    toFieldId: 'actorId',
    and: [{
      kindId: 'MovieGenre',
      fromFieldId: 'movieId',
      toFieldId: 'movieId',
      filters: [{
        fieldId: 'name',
        op: '==',
        value: {STRING: 'action'}      
      }]
    },{
      kindId: 'Actor',
      fromFieldId: 'actorId',
      toFieldId: 'id',
      filters: [{
        fieldId: 'name',
        op: '==',
        value: {STRING: 'Harrison Ford'}      
      }]
    }]
  }]
}
```

## Field Projections and Aggregates <a id="KindQueries-FieldProjectionsandAggregates"></a>

Following the OpenCRUD standard: [https://github.com/opencrud/opencrud](https://github.com/opencrud/opencrud)

Putting aggregates into KindQueries that are similar to OpenCRUD you only allow aggregates at the outer most context, however you allow reference to fields returned by inner queries.

This requires

* Some way to alias the fields of the inner query - "alias".
* A way to specify the projection - "projection".

Example

```
const query = {
  kindId: 'Movie',
  filters: [{
    fieldId: 'releaseYear',
    op: '>',
    value: {INT: 2000}
  }, 
  and:[{
    alias: "actors",
    kindId: 'MovieActor',
    fromFieldId: 'id',
    toFieldId: 'actorId'
  }],
 
  projection: [{
    op: SUM,
    alias: 'actors',
    fieldId: 'age'
  },
  {
    op: COUNT
  }]
}
```

Aggregate and none aggregate ops can not be mixed in a projection.

You can allow "distinct"; it always occurs after the projection as a result it will not affect aggregate ops.

```
enum AggregateOp {
  MIN,
  MAX,
  SUM,
  COUNT,
}
 
input FieldProjectionInput {
  """one of the following is required"""
  fieldId: ID
  fieldName: String
  alias: String
  op: AggregateOp
}
 
input KindQueryInput {
  """from kind (one of the following is required)"""
  kindId: ID
  kindName: String
  alias: String
 
  """projected fields"""
  projection: [FieldProjectionInput]
  """distinct Projected result"""
  distinct: Boolean
 
  """filters (where)"""
  fieldFilters: [FieldFilterInput]
 
  """conjunction (where)"""
  and: [KindQueryInput]
 
  """disjunction (where)"""
  or: [KindQueryInput]
 
  """join (if conjunction or disjunction)"""
  fromFieldId: ID
  fromFieldName: String
  toFieldId: ID
  toFieldName: String
  take: Int
}
```

## Semantics of Join <a id="KindQueries-SemanticsofJoin"></a>

All joins to children are inner joins.

A parent can refer to children using a List of ID's, in this case the results are denormalized, so replication of the parent will occur in the returned result.

This can be used to count the number of instances of a child Kind.

