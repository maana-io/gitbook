# Creating an Entity Extractor

## About this Tutorial

The entity extractor calls the NER service, but allows the user to specify a kind as input. The results are stored in kinds and links. The following mutation uses extractAndLink to both extract, store data and create links. 

## Creating an Entity Extractor

1. First upload a csv file to maana \(in this case [DrillingReport.csv](https://github.com/maana-io/q-tutorials/blob/master/maana-entity-extractor/DrillingReport.csv)\).
2. Record the kindId for the created kind and we will compute the entities in the "comment" field. 
3. In the services inventory, drag the extractAndLink function from the Maana Entity Extractor onto the workspace. 
4. Copy the id from the "DrillingReportscsv" kind. 
5. Select the extractAndLink function and click on the arrow button on the right hand side panel. 
6. Fill in kindId with the kind id for "DrillingReportscsv" in the fieldName set the value to "comment" and press the run button. The results are shown below:

![Figure 1: View after running the extractAndLink function on the &quot;comment&quot; field of the kind &quot;DrillingReportscsv&quot;.](../../.gitbook/assets/image%20%2826%29.png)

7. The kind will now have several "hasEntity" links that link to the kinds where the entities are stored:

![Figure 1: View after uploading CSV and running the entity extractor on the kind. The hasEntities links at the bottom of the kind are the extracted entities.](../../.gitbook/assets/image%20%2876%29.png)

8. Clicking on the PhysicalQuantity link to produce the Physical Quantity kind, and then making sure the Physical Quantity kind is selected, the following view should be visible - showing the extracted Physical Quantity data.

![Figure 1: View showing the Physical Quantity kind and some of the entities that were extracted.](../../.gitbook/assets/image%20%284%29.png)

Many other entities are extracted based on the entities defined in the maana-ner service include Person, Location and Organization. The extracted data can now be used as part of a larger pipeline.

