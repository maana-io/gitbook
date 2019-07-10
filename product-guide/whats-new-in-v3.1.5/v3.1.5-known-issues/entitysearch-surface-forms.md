---
description: >-
  EntitySearch by all surface forms missing matches for Entities if surface
  forms are linked by multiple entities.
---

# EntitySearch - Surface Forms

{% tabs %}
{% tab title="Description" %}
**1. Given at least 1 document and 2 entities called "BookRefA" and "BookRefB".  
2. Given these surface forms:**

```python
      { id: "SF1", name: "a Vice President" }
      { id: "SF2", name: "the Vice President" }
      { id: "SF3", name: "the President" }
      { id: "SF4", name: "and other" }
      { id: "SF5", name: "all other" }
```

#### 3. Add links between entities to surface forms:

RefA1 -&gt; SF2  
RefA3 -&gt; SF4  
RefB1 -&gt; SF4  
RefB1 -&gt; SF5

{% hint style="info" %}
NOTE: SF4 has two linked entities
{% endhint %}

#### 4. Given the document's contents in JSON:

```python
{
    "c": "Docpcavm",
    "id": "Docmdmlh",
    "title": "All Other Vehicle and Other Stores. Supermarkets and Other Grocery All Other Food"
}
```

#### 5. Execute an EntitySearch query using all entities and all surface forms:

```python
query entitySearch_allEntities_docs(
  $docId: ID!
  $docTextId: ID!
  $entity_1_Id: ID!
  $entity_2_Id: ID!
) {
  entitySearch(
    input: {
      scopeKindId: $docId # id of the document kind
      scopeFieldId: $docTextId # id of the field in the document kind
      entitySurfaceForms: [
        {
          kindId: $entity_1_Id # id of Entity 1 kind
        }
        {
          kindId: $entity_2_Id # id of Entity 2 kind
        }
      ]
    }
  ) {
    ...entitySearchResultInfo
  }
}
```
{% endtab %}

{% tab title="Repro Steps" %}
See description, then read below:

1. Teamcity run: 
2. Test case Cli Search Test" -&gt; "Search Shared Surface Forms"
{% endtab %}

{% tab title="Expected Result" %}
RefB1 should have 4 locations:

```python
{
  "data": {
    "entitySearch": [
      {
        "scopeKindId": "62c206b0-0e7f-4c19-8949-2840c8f00304",
        "scopeFieldId": "01a6d0a3-54fd-41a6-94b0-e7dea1d4c5bb",
        "scopeInstanceId": "Docmdmlh",
        "cooccurrences": [
          {
            "kindId": "cf628bdb-c563-42f9-a381-4f6c50539a85",
            "instanceId": "RefA3",
            "locations": [
              3,
              7
            ]
          },
          {
            "kindId": "dbf69a97-d541-466a-81a8-8b9ee10c9190",
            "instanceId": "RefB1",
            "locations": [
              0,
              3,
              7,
              10
            ]
          }
        ]
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Actual Result" %}
RefB1 has 2 locations only for "all other" missing "and other":

{% hint style="info" %}
NOTE: RefA3 found the "and other" at 3,7 locations
{% endhint %}

```python
{
  "data": {
    "entitySearch": [
      {
        "scopeKindId": "62c206b0-0e7f-4c19-8949-2840c8f00304",
        "scopeFieldId": "01a6d0a3-54fd-41a6-94b0-e7dea1d4c5bb",
        "scopeInstanceId": "Docmdmlh",
        "cooccurrences": [
          {
            "kindId": "cf628bdb-c563-42f9-a381-4f6c50539a85",
            "instanceId": "RefA3",
            "locations": [
              3,
              7
            ]
          },
          {
            "kindId": "dbf69a97-d541-466a-81a8-8b9ee10c9190",
            "instanceId": "RefB1",
            "locations": [
              0,
              10
            ]
          }
        ]
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

