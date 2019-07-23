# Understanding Kinds

## Understanding Maana Kinds <a id="understanding-maana-kinds"></a>

Kinds are the term that Maana uses for the concepts used to build their Knowledge Graphs. These "concepts" may contain fields containing Properties, Instances with Values \(e.g. measurements of size, numbers, etc.\) for Entities within them, and the Relationships \(connections/dependencies\) to other Kinds.

| **Term** | **Definition** | **Example** |
| :--- | :--- | :--- |
| **Kinds** | Kinds are concepts | People, Ship, Well, Location, Invoice, etc. |
| **Fields** | Properties within a concept | Fields related to People: name, age, gender, height, weight, etc. |
| **Field Type** | Scalar or another Kind | Scalars: ID, String, Int, Float, Boolean. A list of all custom scalars can be found [here](../../../reference-guide/technical-design-and-architecture/custom-scalars-supported-by-maana-q-platform.md). |
| **Instances** | Values for entities within a Kind | People Instance: Paul Smith, 19, male, 6'0", 200 lbs, etc. |
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

Let's go through each of the different parts of the Kind node in more detail.

#### Kind Schema

The Kind Schema portion of the node contains all of the fields and their types \(including modifiers\) within the Kind's schema. Instances of the Kind will have fields matching the schema. The Field column contains the name of the Field, the Type column contains the type the values of the Field. When Instances are added to the Kind, the values in each of the fields must match the Type definition of the field. For example, a number can't be put in a field that has a type set to String.

There are also two modifiers indicated in the Type column: required and list. If the Type has an exclamation mark \(!\), the field is required to have a value. If the Type is surrounded in square brackets \(\[\]\), the field value is a list. Note that both can be present. Thus \[STRING!\]! means the field is a list of Strings, where each value in the list cannot be null and the list itself must not be null.

#### Kind Links

The Kind Links portion of a node contains relations between the Kind and other Kinds and Instances. The Field column contains the type of relation. It is displayed in the form &lt;field name&gt;.&lt;relation name&gt;. The Type column contains the name of the Kind or Instance that the Link points to. 

For example, the first Link in the screenshot above has **id.hasClassification** in the Field column. This means, the Link exists on the **id** field and the relation is of type **hasClassification**. 

{% hint style="info" %}
Relations are defined as Instances of the Relation Kind.
{% endhint %}

The Type of the first Link is **Categorical**. This means that the Link points to the Categorical Kind.

When you put this all together, this Link has the meaning: the **Locationcsv** Kind's **id** field has a classification of **Categorical**.

Links are most often created automatically by Bots running within the Q platform.

For more details on Links, see

{% page-ref page="../../../reference-guide/technical-design-and-architecture/links.md" %}

For more details on Bots, see

{% page-ref page="../connecting-bots-and-assistants.md" %}

#### Inbound Relations

Inbound relations connect to the ports on the left side of the Kind node. There are two types of relations \(ports\) on the left side: Kind level and Field/Link level.

Kind level relations connect to the topmost port on the left side \(next to the collapse/expand toggle\). Any incoming relations to the Kind will have an edge in the graph from a port on the other Kind to this port.

![Example incoming Kind level relation](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Kind%20Level%20Incoming%20Relation.png)

Field level relations connect to the port next to the field that is part of the relation. Link level relations connect to the port next to the Link that is part of the relation.

![Example incoming Link level relation](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Link%20Level%20Incoming%20Relation.png)

{% hint style="info" %}
In collapsed mode, all edges indicating relations move to the Kind level \(top\) port.
{% endhint %}

![Edges indicating relations move to the top port when nodes are collapsed](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Collapsed%20Nodes.png)

#### Outbound Relations

Just like there are two types of inbound relations, there are two types of outbound relations: Kind and Field/Link. The outbound relations of a Kind node connect to the ports on the right side of the node.

Kind level relations are indicated by edges in the graph that connect to the top right port \(next to the expand/collapse button\).

Field level relations connect to the port next to the field that is part of the relation. Link level relations connect to the port next to the Link that is part of the relation.

![Example of an outbound field level relation](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Field%20Level%20Outgoing%20Relation.png)

Field level relations indicate that a field has a type that is a Kind.

{% hint style="info" %}
Note there is a difference in style between edges in the graph that indicate field level relations \(blue\) and the edges that indicate link level relations \(gray\).
{% endhint %}

#### Relation Indicators

The fields and links with relations have an indicator in the port.

![The Link indicator in the port](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Link%20Indicator%20in%20Node.png)

This indicates a Link to another Kind or Instance. Hovering the mouse over the port with display a preview of the Kind or Instance that is on the other end of the Link.

![Example Kind preview on hover](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Link%20Hover%20Kind.png)

Clicking the link icon in the port will automatically add the linked Kind to the graph.

### In-node Editing

To edit the properties of the Kind, click on the pencil icon in the top right corner. \(An alternative way to enter edit mode is to double click on the node.\) This opens the in-node editing view.

![Kind node in-node editing view](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Kind%20Node%20In-Node%20Editing%20View.png)

{% hint style="info" %}
You can only edit Kind nodes that were created in the currently open Workspace.
{% endhint %}

Here you can change the name of the Kind, the name of the fields, the types of the fields, and the modifiers applied to each field. You can also add or remove fields from the Kind. Clicking the Save button will save any modifications. Clicking the Cancel button will discard the changes.

{% hint style="info" %}
If the Kind has any Instances, you will only be able modify the Type of the fields between _compatible_ types. Compatible types are String, ID, JSON, and any Kind type.
{% endhint %}

### Editing in the Schema Editor Assistant

The Schema Editor Assistant allows editing of a Kind's schema with some additional options not available in in-node editing. To open the Schema Editor Assistant, select the Kind to edit and choose Schema Editor in the Assistants panel.

![Editing a Kind&apos;s schema in the Schema Editor Assistant](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Schema%20Editor.png)

Here you will be able to perform the same actions that you can in in-node editing \(modifying the Name, Type, and Modifiers of each field, along with adding or removing fields\) but you will find some additional fields as well. Most of the fields are not currently used, however there are a couple that can provide some additional functionality.

* **Description** - This field allows adding a description of the field. Note that this is only shown in the Schema Editor.
* **Read Only** - Selecting this will make the field unmodifiable in both the Schema Editor and the in-node editing. \(Note that the **Read Only** flag itself remains modifiable so that you can make the field editable again if needed\).

![Example of setting a field to Read Only](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Read%20Only%20Field.png)

Save changes by clicking the save icon in the top left or discard changes by clicking the cancel icon.

### Editing in the Context Panel

The Information pane of the Context panel allows viewing and editing some additional properties of the Kind.

![Example of the Information pane of a Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Information%20Pane%20-%20Kind.png)

The following properties are editable:

* **name:** the name of the Kind. This is the same name when editing in-node.
* **description:** Use this to provide more information about the Kind that would help someone else understand the concept the Kind represents. \(This is only shown in this location in the UI\)
* **thumbnailUrl:** This allows specifying a different URL for the thumbnail image. Note that the thumbnail image is only shown here in the UI.
* **isPublic**: Not currently used
* **nameField:** When viewing Instances of the Kind \(whether in the Workspace or in search results\), this tells the UI the name of the field whose value should be used as the name of the Instance. \(Basically, which field to use as the name for the Instance\). If this is left unset, the UI will try to determine the name of the Instance automatically. If it fails, it will default to the ID.

The un-editable properties include:

* **id**: the ID of the Kind
* **serviceId:** The ID of the service the Kind comes from
* **isManaged:** Not currently used

The Information pane also includes a quick view of the schema of the Kind, similar to what you would see in the Kind node on the graph.

![Schema view in the Information pane](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Information%20Pane%20Schema%20View%20-%20Kind.png)

