# Inside the Workspace

The workspace features several areas with specific functionality that enables you to create, manage, visualize and explore Knowledge Graphs and their components.

![Overview of a Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspace%20Overview.png)

{% hint style="info" %}
**Note**:  Most actions that are taken in a workspace will be auto-saved.  Changes that need to be explicitly saved, such as those made in the Context Panel or Assistant Panel, will have a save button.  Contact Maana support to resolve any issues with saving.
{% endhint %}

## Explorer Panel Area

This area contains Knowledge Graphs \(KGs\) and the Kinds, Functions, and Instances of various types that are a part of the Knowledge Graphs. It also contains Function implementations, along with the Functions that are a part of the implementations. The Explorer Panel area of the screen allows you to:

Select or navigate a hierarchical list of:

* Knowledge Graphs
* Files
* Documents
* Kinds
* Functions \(and their implementations when applicable\)
* Instances

### **Explorer Panel** enables you to:

* Create a new Knowledge Graph.
* Upload local files into the Workspace.
* Upload a remote file into the Workspace.
* Remove or delete items from your Workspace.



![The buttons at the top of the Explorer panel allow you to perform the Actions described above](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Explorer%20Panel%20Buttons.png)

## The Canvas Area

The **Canvas Area** offers you the ability to visualize Knowledge Graphs and Function implementations. Within Knowledge Graphs you can see Kinds, Functions, and Instances as nodes on the graph and the Relations between them as edges. In addition, you can create a new Kind or Function, or remove or duplicate a node \(Kind, Function, or Instance\) in this location.

![Canvas area overview](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Canvas.png)

### The Canvas area of the screen enables you to:

#### Drag and drop files to enhance a Knowledge Graph

Dragging and dropping files is supported in the Canvas area when a Knowledge Graph is shown.

* Files are uploaded and an instance of the File kind is created when dropping a file on the graph. A File node representing the uploaded file is added to the Knowledge Graph as well.
* Certain file types have special viewers in the Assistants panel that allow previewing the data
  * These include CSVs, TXTs, PDFs, and Images
* Some file types have special meanings:
  * CSV
    * Uploading a CSV generates a Kind with fields corresponding to the columns of the CSV \(this requires the CSV to have a header row\)
    * Each row in the CSV becomes an Instance of the generated Kind
  * Documents \(PDF, DOCX, XLSX, TXT\)
    * Uploading these file types create an Instance of the Document Kind in addition to the Instance of the File Kind
  * Images \(JPG, PNG\)
    * Uploading these file types create an Instance of the Image Kind in addition to the Instance of the File Kind

#### Create new Kinds and Functions

The first two buttons in the action panel allowing creating a new Kind or Function, respectively. Newly created Kinds and Functions start out with an empty schema and an auto-generated name. Define the fields \(names, types, and modifiers\) that make up the schema directly in the node shown on the graph.

![Edit views of a newly created Kind and Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/In-node%20Editing.png)

{% hint style="info" %}
Kinds and Functions must have unique names within a Workspace and they must adhere to the GraphQL naming conventions.
{% endhint %}

{% hint style="info" %}
Fields within Kinds and Functions must have unique names and they must adhere to the GraphQL naming conventions.
{% endhint %}

For more info about Kinds and Functions see the following links:

{% page-ref page="../building-knowledge-layers/kinds-and-functions/" %}

{% page-ref page="../building-knowledge-layers/understanding-functions.md" %}

#### Duplicate Kinds, Functions, and Instances

Kinds, Functions, and Instances can be duplicated within the Canvas area by selecting one or more and clicking the duplicate button in the Action Buttons:

![Duplicate button](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Duplicate%20Icon.png)

Duplicating a Kind, Function, or Instance creates an exact copy and adds a corresponding node to the graph. In the case of Kinds and Functions, a new, unique name is generated.

#### Remove Kind, Function, and Instance nodes from the graph

Kind, Function, and Instance nodes can be removed from the graph by selecting one or more and clicking the remove button in the Action Buttons:

![Remove button](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Remove%20Icon.png)

This will remove the Kind, Function, or Instance node from the graph.

{% hint style="info" %}
Removing a Kind, Function, or Instance node from the graph does not remove the Kind, Function, or Instance from the Workspace. It only affects the current graph.
{% endhint %}

#### Edit existing Kinds and Functions

The pencil icon in the top right corner of nodes allows editing the schema of the Kind or Function.

![Edit Icon is in the top right](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Kind%20Editing.png)

{% hint style="info" %}
Only Kinds and Functions created in the current Workspace are editable in that Workspace. Kinds and Functions brought in from other services are not.
{% endhint %}

#### Compose Functions

The composition of a Function can be viewed and edited by clicking the expand icon in the top right of the Function node.

![Click the Expand Icon to view the composition of a Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Function%20Decomposition%20Button.png)

{% hint style="info" %}
Only Functions created in the current Workspace can have their composition viewed and modified within that Workspace. Functions brought in from other services cannot.
{% endhint %}

Function composition is a whole topic in itself. See the following link for a detailed description of Function Composition:

{% page-ref page="../building-knowledge-layers/modeling-problem-questions/about-function-modeling/composing-functions.md" %}

#### Navigating Links between Kinds and Instances

One of the most important aspects of the Knowledge Graph is the ability to view and navigate the links between Kinds and Instances. When a Kind or Instance has a link to the another Kind or Instance, a link icon will display next to the field that has the link.

![Link Icon on a File node indicating a link to the &quot;testcsv&quot; Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/File%20Node%20with%20Link.png)

Hovering over the link Icon will display a preview of the Kind or Instance that the link points to.

![Hovering over the link displays a preview of the &quot;testcsv&quot; Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Link%20Port%20Hover.png)

Clicking the link icon will add the linked Kind or Instance to the graph. A line will be drawn from the linked field to the Kind or Instance that it points to, indicating the relationship between the two.

![The line indicates the relationship between the &quot;hasKind&quot; field and the &quot;testcsv&quot; Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/File%20to%20Kind%20Link.png)

The darker background color on the linked row indicates the link is from a Relation \(see info box below\). The relation name is "hasKind" and the value is the Kind it points to \(testcsv in this case\). The Relation can be read as "test.csv has Kind testcsv". \(pretty cool huh!\)

{% hint style="info" %}
There are two types of links shown between Kinds and Instances:

* When a field in a Kind has its type set to a Kind
  * Displayed next to the field
* When there is a Relation between a Kind or Instance and another Kind or Instance
  * Displayed as a separate row after the fields in the Kind or Instance with a slightly different background color
{% endhint %}

#### Zoom to fit

Finally, there is a handy little button that will expand the viewable area of the canvas \(zoom out\) to fit all of the nodes currently in the graph.

![Zoom to fit icon](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Zoom%20to%20Fit%20Icon.png)

## The Context Panel

Use the **Context Panel** has panes to view or edit properties of Kinds, Functions, and Instances, view links, view Bots, and run Functions.

### **Information pane**

The Information pane allows viewing and modifying properties of everything in the Workspace, including Kinds, Functions, Instances, Knowledge Graphs, services, and the Workspace itself.

![Information pane for a Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Kind%20Info%20Pane.png)

Properties that are not editable are disabled. Changes made in this view can be saved or discarded using the buttons at the top of the pane.

![Save and Discard buttons at the top of the Information pane](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Save%20Discard%20Icons%20Info%20Pane.png)

{% hint style="info" %}
Only Kinds and Functions created within the current Workspace are editable in the Information pane. Kinds and Functions brought in from other services are not. 
{% endhint %}

### Links pane

The Links pane displays the Relation based links on the selected Kind or Instance. Selecting one or more and clicking the add button will add the linked Kind\(s\) or Instance\(s\) to the active Knowledge Graph. The Links are organized by Outbound links \(links from the selected Kind or Instance that point to another Kind or Instance\) and Inbound links \(links from another Kind or Instance that point to the selected Kind or Instance\).

![Example Links pane that contains one Outbound Link](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Links%20Pane.png)

### Bots pane

The Bots pane is used to see any Bots that are available for the current selection and the status of the Bot \(running, stopped, etc.\). If the Bot has an associated Assistant, a button is shown that will open the Assistant in the Assistants panel.

![Example Bots pane with a single Bot that has an Assistant](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Bots%20Pane.png)

### Run pane

The Run pane has a special purpose. It is used to run Functions with provided sample data. It is only available when a Function is selected. To run a Function, fill in values for the fields \(at a minimum the required fields must have values\), and click the Run button.

![Example Run panel with a required field, list field, and optional field](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Run%20Function%20Pane.png)

Running a Function has many options and nuances of which to be aware. These are explored in more detail at the link below:

{% page-ref page="../building-knowledge-layers/modeling-problem-questions/about-function-modeling/running-functions.md" %}

## The Inventory Panel

The Inventory Panel can be thought of as the pallet containing everything in the Workspace. It contains the services, files, documents, Kinds, Functions, and Instances that have been created within the Workspace or brought in to the Workspace from another service. It is organized by type as shown below.

![Example of the Inventory Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspace%20Inventory.png)

{% hint style="info" %}
Notice the Auto-Generated groups under Kinds and Functions. These are Kinds and Functions that are automatically created for the Kinds created within the Workspace. The Functions can be used to create, read, update, or delete Instances of the Kinds created in the Workspace.
{% endhint %}

Files, documents, Kinds, Functions, services, and Instances can be brought into the Workspace by dragging them from the Search results and dropping them into the Inventory. In a complex Workspace, there could be hundreds of things in the inventory. The search box at the top allows searching the inventory by name.

## The Assistant Panel

The Assistant Panel will show Assistants based on the current context. In 3.2.0, the context is just the current selection in the Workspace. Selecting an Assistant from the drop down menu will provide additional functionality. For example, when selecting a CSV file there is a File Viewer Assistant that will show the contents of the file in a table. When selecting a Kind, there is a Data Preview Assistant that will show all of the Instances in the Kind.

Some Assistants include:

* File Preview - Shows when a file is selected. Preview a file.
  * CSV, TXT, PDF, and Images are supported
* Data Preview - Shows when a Kind is selected. Preview instances in the Kind.
* Function Results - Shows when a Function  is selected. Displays the results when running a Function.
* GraphQL IDE - Shows when a Workspace is selected. Allows executing GraphQL queries against the Workspace service \(such as querying for instances of a Kind\)
* Maana Field Classifier Assistant - Works with Kinds. Displays classifications of fields in the Kind based on Instances in the Kind. Allows changing the type based on the classification. \(this Assistant must be added to the Workspace to show up\)

![Example showing the &quot;GraphQL IDE&quot; Assistant with a Workspace selected](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Assistant%20Selection%20Drop-down.png)

{% hint style="info" %}
Assistants that are provided as a service \(such as the Maana Field Classifier Assistant\) must be added to the Workspace \(by dragging and dropping from Search into the Inventory panel\) before they will be available for selection in the Assistants panel.
{% endhint %}





