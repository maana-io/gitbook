# Fact Recognition Bot Tutorial

## About this Tutorial <a id="about-this-tutorial"></a>

The Fact Recognition Bot uses the Fact Recognition service to extract facts from kinds and store them in Maana.

{% file src="../../../.gitbook/assets/wellremarks.csv" caption="WellRemarks.csv" %}

## Using Fact Recognition Bot for Kind Information Extraction <a id="1-creating-a-fact-recognition-bot"></a>

The simplest way to apply information extraction is to use the mutation extractTriples and apply it to a kindId and a fieldName.

1. Apply triple extraction to the file WellRemarks.csv \(attached above\) which should be loaded onto the workspace.
2. A kind will be created named "WellRemarkscsv", copy that kind id.
3. Import Fact Recognition Bot by searching for it and dragging it into the workspace
4. Drag the extractTriples function from the the Maana Fact Recognition Bot in the service inventory onto the workspace.
5. Click the arrow button on the right hand panel and enter the kindId of the "WellRemarkscsv" kind.
6. Fill out the rest of the fields as shown below, and press the run button.

The result should look like that in the figure below.

![](../../../.gitbook/assets/image%20%2875%29.png)

1. The triples are extracted from the kind specified by 'kindId' in the provided fieldName and then stored in the kind 'PatternMatchResult'.
2. Search for the kind PatternMatchResult to see the entries from the extraction.

![](../../../.gitbook/assets/image%20%2877%29.png)

### Fact Extraction With Pattern Filter <a id="fact-extraction-with-pattern-filter"></a>

In order to use the fact extraction service \(information extraction\) you need:

1. A kind containing text fields from which you will extract facts \(shown below as ThisKind\).
2. A kind that contains the desired patterns you wish to extract \(shown below as Pattern\). The schema of the pattern kind is 3 string lists named predicateLemmas, subject and object. The predicateLemmas is a list of predicates "\[buys,bought,are\]", the service expands these predicates to include related words. The predicateLemmas can have any values, the subject and object however, are restricted to values accepted in the entity extractor - the catch all is "\["ANY"\]", but can more generally be "\["PERSON","LOCATION","ORGANIZATION",...\]"

#### Creating The Patterns Kind <a id="creating-the-patterns-kind"></a>

The Pattern kind \(which can have any name\) can be created manually.

1. Add a new kind to the workspace \(name it "Pattern"\), edit the schema to include "predicateLemmas" of type String with modifier LIST, "object" of type String with modifier LIST and "subject" of type String with modifier LIST.
2. Once the kind is created, functions for the kind should be visible in the service inventory. Your workspace should look like that below:

![](../../../.gitbook/assets/image%20%28120%29.png)

There will be a set of functions for every Kind in your workspace. These functions can be used to manipulate the Kinds.

1. Drag the addPattern function onto the workspace. In this case set predicateLemmas to "buy" and set subject and object to "ANY" as below.

![](../../../.gitbook/assets/image%20%2857%29.png)

Fill in the pattern information for the addPattern information.

{% hint style="info" %}
Remember, to set the predicateLemmas to a relation/relations that you expect to have in your data. "are" for example is a very common relation.
{% endhint %}

#### Creating the kind to extract data from <a id="creating-the-kind-to-extract-data-from"></a>

1. Next, upload a csv file where at least one of the fields contains text with relations in it - or you can create a kind manually and add the text "Alex bought a bike".
2. Next create a kind containing the text you wish to extract - call it "ThisKind". It should have a field called "Text", and should have an instance with the the value "Alex bought a bike".

![](../../../.gitbook/assets/image%20%2888%29.png)

Add text to the "ThisKind" kind with the addThisKind function.

1. After you have have created the 2 kinds you can run the fact recognition bot.

#### Running extractByPattern <a id="running-extractbypattern"></a>

1. First, search for the "Maana Fact Recognition Bot" and drag it to the services inventory.
2. Drag the extractByPattern function onto the workspace.
3. Use the extractByPattern function, the fieldName is "Text", but that should be the name of the field containing the text you want to extract.\) Notice that below, kind ID's are used and not names. "kindId" refers to the ID for "ThisKind" and "patternID" refers to the ID for "Pattern".

![](../../../.gitbook/assets/image%20%2860%29.png)

Result of running the extractByPattern function on the "Pattern" and "ThisKind" kinds

1. This will extract facts from the kind "ThisKind" in field "Text" using the patterns defined in "Pattern". The results of the query will be a bot action. The extracted facts will be stored in the kind "PatternMatchResults" and links back to "ExtractTestKind" and "TriplePatterns" will also be generated.

#### How to see the results? <a id="how-to-see-the-results"></a>

The results are stored in the system kind \(kind automatically generated at startup\) called PatternMatchResult. All patterns are appended to this kind with links back to the original data and to the pattern that was used to extract the data. For this particular case, the result is the following "subject","predicate","object" in the PatternMatchResult Kind:

![](../../../.gitbook/assets/image%20%2835%29.png)

Result shown in the PatternMatchResult kind.

## Structure Mapping \(Extraction by Example\) / Slot Filling <a id="3-structure-mapping-extraction-by-example-slot-filling"></a>

You can also extract data by example \(slot filling\) using structure mapping. In this case, you want to extract information from text similar to "Carl bought a fish for 5 dollars at the store" and store the information in a kind with fields "name","object","price","location".

You need to provide example\(s\) and your associated mapping\(s\). The example would be "Carl bought a fish for 5 dollars at the store", the mapping is:

```text
{ "name": "Carl", "object": "fish", "price": "5 dollars", "location": "store" }
```

The example sentence is compared to a data source and results are extracted and stored in a kind. The interface for this capability is implemented with 2 different mutations: 1. You need to specify the kindId \(the source of the text where data will be extracted from\), storageKindId \(the location where the extracted data will be stored\), the fieldName \(the name of the field in kindId to be used\), the example sentence \(example\) and the mapping to tell how the different terms in the example sentence map to the kind.

```text
extractByExample(kindId: ID, fieldId: ID, storageKindId: ID, fieldName: String, storageKindName: String, kindName: String, mapping: [CorrespondenceInput], example: String): [ID]
```

1. Instead of an example, mapping and storageKind a "exampleKind" is provided which contains the same information. The exampleKind contains a list of examples, their mappings and the target kind. The results are stored in their respective kinds:

```text
extractByExampleKind(kindId: ID, fieldId: ID, exampleKindId: ID, kindName: String, fieldName: String, exampleKindName: String): [ID]
```

In order to experiment with these tools:

1. Upload the file simpleFacts.csv \(attached under the heading of this section\) into Maana and store the Id of the associated Kind it creates.
2. Create a kind to store the results in, name this kind "PurchaseEvent" and it should have the schema "{name : "STRING", object : "STRING", price : "STRING", location : "STRING"}.

### Mutation 1 <a id="mutation-1"></a>

With those two kinds created we can perform the first query and see the results. 1. Below the kindId should be the Id for "SimplefactsCSV" and the storageKindId should be the id for "PurchaseEvent".

1. In this query, the mapping is specified as an list of name/value GraphQL objects:

```text
mutation a {extractByExample(  kindId: "bbcb2d1f-1c0c-4d81-adff-39de27d8fc52", #your SimplefactsCSV Kind Id    fieldName : "Text",    mapping : [      {name : "name", value : "Carl"},      {name : "object", value : "fish"},      {name : "price", value : "5 dollars"},      { name : "location", value : "store"}      ],    example : "Carl bought a fish for 5 dollars at the store",    storageKindId : "e81846a4-ca93-4947-b8f2-57fb92ecb957" #your PurchaseEvent Kind Id    )}
```

1. The result should be several entries in the "PurchaseEvent" kind - as below:

![](../../../.gitbook/assets/image%20%2871%29.png)

### Mutation 2 <a id="mutation-2"></a>

In order to perform the second mutation you need to create an additional kind to store the example and mapping information. 1. Create a new kind and call it "exampleContainer". The "exampleContainer" should have schema:

```text
{  example :  STRING,  mapping : STRING,  required : [STRING],  kind : STRING,  kindId : STRING}
```

1. Create an instance of the "exampleContainer" with the following mutation below, where kindId is the id of the purchaseEvent kind:

```text
mutation e {addexampleContainer(  input: {    example: "Carl bought a fish for 5 dollars at the store.",    mapping : "{\"name\" : \"Carl\", \"object\" : \"fish\", \"price\" : \"5 dollars\", \"location\" : \"store\"}", #This has to be a serialized (stringified) JSON    required : ["name","object"],    kindId : "2215a0af-99de-49af-8892-a518cb77e17f" #Your purchaseEvent Kind ID    }    )}
```

1. After the instance is created, the following query can be performed: Upload a new file [otherFacts.csv](https://github.com/maana-io/q-tutorials/blob/master/maana-fact-recognition-bot/otherFacts.csv) and use the kindId generated there, in the mutation below \(if you do not use a new kind, the same facts will be extracted and no new entries will be added\):

```text
mutation {  extractByExampleKind(    kindId : "bbcb2d1f-1c0c-4d81-adff-39de27d8fc52", #your otherFactscsv Kind ID    exampleKindId : "5f006487-74a5-4797-beba-17d0a5cb5a5e", #your exampleContainer Kind ID    fieldName : "text"    )    }
```

![](../../../.gitbook/assets/image%20%2839%29.png)

Result after the extractByExampleKind function is run.

1. The result will be several entries in the "PurchaseEvent" kind. These can be viewed as below:

![](../../../.gitbook/assets/image%20%28125%29.png)

Result shown in the PurchaseEvent kind.

