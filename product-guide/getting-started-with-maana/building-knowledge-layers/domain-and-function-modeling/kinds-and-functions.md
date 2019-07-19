# Understanding Kinds and Functions

## Understanding Maana Kinds <a id="understanding-maana-kinds"></a>

Kinds are the term that Maana uses for the concepts used to build their Knowledge Graphs. These "concepts" may contain fields containing Properties, Instances with Values \(e.g. measurements of size, numbers, etc.\) for Entities within them, and the Relationships \(connections/dependencies\) to other Kinds.

| **Term** | **Definition** | **Example** |
| :--- | :--- | :--- |
| **Kinds** | Kinds are concepts | People, Ship, Well, Location, Invoice, etc. |
| **Fields** | Properties within a concept | Fields related to People: name, age, gender, height, weight, etc. |
| **Field Type** | Scalar or another Kind | Scalars: ID, String, Int, Float, Boolean. A list of all custom scalars can be found [here](../../../reference-guide/technical-design-and-architecture/custom-scalars-supported-by-maana-q-platform.md). |
| **Instances** | Values for entities within a concept | People Instance: Paul Smith, 19, male, 6'0", 200 lbs, etc. |
| **Values** | A particular size, measure or number within an entity | Values for Paul: 19 yrs. old, 200 lbs., , 6'0", etc. |
| **Relations** | Connections/dependencies that can be established between fields of different Kinds | Married to Linda Smith, related to family name Smith. |

Kinds in Maana fall into four categories

1. **Raw Data Instances**
2. **Interpreted Data Kinds**
3. **Manually Created Kinds**
4. **Types imported via an added service**

### Raw Data Instances <a id="raw-data-kinds"></a>

Raw Data Instances have data that represents files \(csv, jpeg or png\) or documents \(pdf\) that have been uploaded into Maana \(via the portal or CLI\) and their corresponding metadata.

![Raw Data Instance](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Raw%20Data%20Instance.png)

### Interpreted Data Kinds <a id="interpreted-data-kinds"></a>

Interpreted Data Kinds are generated from Raw Data Instances following being parsed by Maana Bots/Microservices. Currently only CSV files will have Interpreted Data Kinds generated from them.

![Interpreted Data Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Interpreted%20Data%20Kind.png)

### Manually Created Kinds <a id="manually-created-kinds"></a>

Manually Created Kinds are defined by you and the schema you desire/define.

![Manually created Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Manually%20Created%20Kind.png)

### Types \(Kinds\) Imported Via an Added Service

External services that have a graphQL endpoint will likely have type definitions that when imported into the Maana platform will be represented as Kinds. The Kind names will be preceded with the service name to help disambiguate between Kinds from different services but with the same name.

![Imported &quot;Person&quot; Kind from &quot;Maana Entity Extractor&quot; service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Imported%20Kind.png)

**Note**: Nodes can be displayed in full or compact mode, and you can toggle between them.

![Nodes in the collapsed view](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Collapsed%20Nodes.png)

### The Structure of a Kind <a id="the-structure-of-a-kind"></a>

The screenshot presented below is an example of how a Kind might appear to you.​

![Structure of a Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Structure%20of%20a%20Kind.png)

To edit the properties of the Kind \(name only\), double click on the Kind node to access in-node editing. 

You can also use the Context Panel mentioned earlier \(refer to example presented below\). Save changes to your Kind by using the blue save icon found at the top of the context panel.

![Editing properties of a kind in the Context Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/KIND%20EDIT.png)

To edit the Kind schema, use in-node editing or the Context Panel \(refer to example presented below\). Save changes to your Kind by using the blue save icon found at the top of the context panel.

![Editing properties of a kind in Context Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/KIND%20SCHEMA%20EDIT.png)

## Understanding Maana Functions

Functions are the term that Maana uses for the problem-question used to build their Knowledge Graphs. Remember the example of "Given x, what is y"? These functions allow you to define x and y and connect them to other functions in meaningful ways to form the computational portion of your solutions and your knowledge graph. In graphQL speak, functions are either queries or mutations.

Functions in Maana fall into two general categories

1. **Authored functions** 
2. **Imported functions**

### Authored Functions

These are created by you by clicking on the "sigma" icon in any knowledge or function graph within a workspace. 

You can edit the schema \(including field modifiers\) of these functions at any given time, although there may be consequences depending on what else they are connected to. 

You can also define the implementation of these functions by clicking through the name of the function which is also a hyperlink and opening its function graph.

### Imported Functions

These are queries or mutations that authors of a service \(accessed via a graphQL endpoint\) have made available for others \(like yourself\) to leverage. 

It's important to note that though these can be incredibly useful in building out your solution, you _cannot_ edit the schema or the implementation \(underlying logic\) of these functions.

### The Structure of a Function <a id="the-structure-of-a-kind"></a>

The screenshot below shows the anatomy of a function

![Function node](https://maanaimages.blob.core.windows.net/maana-q-documentation/n1.png)

Like Kinds, Functions can also be edited via in-node editing \(see screenshot below\)

![Double click on node to enable in-node editing](https://maanaimages.blob.core.windows.net/maana-q-documentation/n2.png)

However, by selecting the function and clicking on the info \(i\) tab in the context panel, you won't be able to edit the schema or field modifiers \(list or mandatory\). Here you will be able to access the id for the function and modify the function name, description and graphqlOperationType \(Query or Mutation\). 

![Function options through the info tab in the context panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/n3.png)

### Field Modifiers

There are two field level modifiers available in Maana functions

1. List - indicates that the field is a list of values
2. Mandatory - indicates that the field is _required_ for the function to execute 

