# Entity Extractor

## What is this service?

Maana Entity Extractor service takes unstructured data \(i.e. text\) and passes it along to [NER Service](named-entity-recognition-ner.md), whereupon it extracts relevant entities that are present in the data and creates [links](../../technical-design-and-architecture/links.md) to them. By default, it recognizes several different types of entities, including:

* Person, location and organization names
* Currency, percentages, and numeric values
* Phone and social security numbers
* Urls and email addresses
* Geospatial coordinates and physical quantities

## Why might you want to use it? 

For each entity mention discovered, the extractor creates links between the originating text and the instance of the entity kind. These links can be used for graph walking and downstream analytics.

## How do you run/invoke it?

The entity extractor service is invoked manually to extract entities. After importing the service\[TBD\]_Link to how to import services_ bring the mutation _extractAndLink_ into the workspace and invoke it on a file/CSV kind with an applicable _text_  field. Because this mutation returns a [Bot Action](../../technical-design-and-architecture/bot-actions/), query relevant BotAction fields:

```graphql
mutation
{
  extractAndLink(kindName:"MY_FILE_KIND.CSV",fieldName:"myTextField"){
    id
    created
    status
    lastUpdated
    errors
  }
}
```

## Example of _extractAndLink_

The following example CSV of comments would be passed into `extractAndLink` with `fieldName = "comment"`:

| id | comment |
| :--- | :--- |
| 0 | "Barry Carlson worked on the Well 12345." |
| 1 | "The Well 12345 was drilled by John Davidson." |
| 2 | "The cost to drill this well was $5,345,345." |
| 3 | "The MD was 19,000 ft." |
| 4 | "External casing diameter was 8.625 inches." |
| 5 | "Well 789 was drilled on June 4th, 2019 by Barry Carlson." |
| 6 | "Well 12345 was used as an offset." |
| 7 | "The depth of Well 12345 was 23,400 feet TVD, with casing strings of 5." |
| 8 | "Drilling was by WellCo, Inc." |

The service will extract the following entity mentions, creating the instances of the kinds if they don't already exist:

| surface form | kind |
| :--- | :--- |
| Barry Carlson | Person |
| 12345 | Number |
| $5,345,345 | Currency |
| 5,345,345 | Number |
| 19,000 ft | Physical Quantity |
| 19,000 | Number |
| 8.625 inches | Physical Quantity |
| 8.625 | Number |
| 789 | Number |
| June 4th, 2019 | Date |
| 2019 | Date |
| 23,400 feet | Physical Quantity |
| 23,400 | Number |
| 5 | Number |
| WellCo, Inc | Organization |

it also creates a link between each of the entities and their originating text. The links can be inspected either via graphQL, e.g.:

## Assumptions

1. Both Maana NER Service and Maana Physical Quantity are available.
2. Kind being processed contain only text.

## More information

See the Maana Cookbook for a tutorial on how to use [Entity Extractor](https://maana.gitbook.io/q/maana-q-cookbook/advanced-recipes/entity-extractor-tutorial)

