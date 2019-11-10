# Entity Extractor Tutorial

## About this Tutorial

The entity extractor calls the [NER service](../../product-guide/reference-guide/q-platform-and-microservices/maana-platform-services/named-entity-recognition-ner.md), but allows the user to specify a kind as input. The results are stored in kinds and [links](../../product-guide/reference-guide/technical-design-and-architecture/links.md). The following mutation uses extractAndLink to both extract, store data and create links. 

{% file src="../../.gitbook/assets/drillingreport \(1\).csv" %}

## Creating an Entity Extractor

1. First upload a csv file to maana \(in this case DrillingReport.csv attached above\).
2. Record the kindId for the created kind and we will compute the entities in the "comment" field. 
3. Import Maana Entity Extractor into the workspace, and then drag the extractAndLink function from the inventory panel onto the workspace. 
4. Copy the id from the "DrillingReportscsv" kind. 
5. Select the extractAndLink function and click on the arrow button on the right hand side panel. 
6. Fill in kindId with the kind id for "DrillingReportscsv" in the fieldName set the value to "comment" and press the run button. The results are shown below:

![](../../.gitbook/assets/image%20%2859%29.png)

7. After the BotAction has completed, the kind will now have several "hasEntity" links that link to the kinds where the entities are stored:

![](../../.gitbook/assets/image%20%2835%29.png)

8. Clicking on the PhysicalQuantity link to produce the Physical Quantity kind, and then making sure the Physical Quantity kind is selected, the following view should be visible - showing the extracted Physical Quantity data.

![](../../.gitbook/assets/image%20%2843%29.png)

Many other entities are extracted based on the entities defined in the maana-ner service include Person, Location and Organization. The extracted data can now be used as part of a larger pipeline.

