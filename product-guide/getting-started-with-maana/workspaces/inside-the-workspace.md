# Inside the Workspace

The workspace features several areas with specific functionality that enables you to create, manage, visualize and explore Knowledge Graphs and their components.

![](../../../.gitbook/assets/screen-shot-2019-07-02-at-2.50.22-pm.png)



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

![The buttons at the top of the Explorer panel allow you to perform the Actions described above.](../../../.gitbook/assets/screen-shot-2019-07-02-at-2.46.05-pm.png)



## The Canvas Area

The **Canvas Area** offers you the ability to visualize Knowledge Graphs and Function implementations. Within Knowledge Graphs you can see Kinds, Functions, and Instances as nodes on the graph and the Relations between them as edges. In addition, you can manually add, remove or clone a Kind in this location - as well as auto-arranging or viewing the entire Graph. You man also reset the Workspace layout from this area.  

### The Canvas area of the screen enables you to:

* Drag and drop files to create/enhance a Knowledge Graph.
* Create, clone or remove Kinds from a Knowledge Graph.
* Create, clone or remove Functions from a Knowledge Graph.
* Navigate to Function Graphs and compose them by appropriately connecting Functions.
* Curate existing Kinds and the connections between them.
* Visualize and manually explore the Knowledge Graph \(including zoom to fit\).

## The Context Panel

![Example of the Canvas screen](https://maanaimages.blob.core.windows.net/maana-q-documentation/image008.png)



Use the **Context Panel** to create Kind names, Property Toggles and edit Schema.  You may also suggest Inbound and Outbound Relations \(hasKind\) to Interpreted Kinds in this location.

### **Context Panel** activities include:

* **Information Tab** - Modification or deletion of Kinds or their properties.
  * Enables you to:
    * Modify Kinds and their properties
    * Delete or completely remove Kinds from the Knowledge Graph.
* **Relations Tab** - Creation of relationships between Kinds or Entities within Kinds.
  * Used to create relations between Kinds or entities within Kinds.

![Example: Information Tab](https://maanaimages.blob.core.windows.net/maana-q-documentation/Information%20Tab.png)



* **Bots Management Tab** - Used for to see if any bots are running for a selected Kind, and change the run state of the bots \(stop if already running, start if not running, navigate to assistant for required input before starting run\). Also see the start time, end time, and error state of bots for the selected kind.

## The Inventory Panel

The Inventory Panel can be thought of as the pallet containing all of the Microservices, Files, Kinds, and pre-populated Core System Services that can be brought into the workspace.

![Example: Relations Tab](https://maanaimages.blob.core.windows.net/maana-q-documentation/Relations%20Tab.png)



### **Inventory Panel** activities include:

* Creating a New Knowledge Graph using the listed **Services**.
* Querying a Knowledge Graph using the listed **Services**.
* Uploading a file or group of files into the Workspace from the listed **Services**.
* Removing a Knowledge Graph from the Workspace.

{% hint style="info" %}
**Note**:  The contents of the Inventory Panel are specifically bound to each individual workspace. So, if you create a new workspace and you want its inventory to mirror that of another workspace, you will need to repeat any efforts you undertook to populate the Inventory Panel of the original workspace.
{% endhint %}

{% hint style="info" %}
**Note**:  The limit on the number of Services that can be added to a single workspace is 1000.
{% endhint %}

## The Assistant Panel

The Assistant Panel allows you to visualize Kinds and data associated with those Kinds like Instances, Entities and Values. Raw Data Kinds can be explored quickly using the Assistant panel, as each entity detected in the data file can be filtered using a “search as you type” capability.

![Example: Inventory Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/image010.png)



### Assistant **Panel** activities include:

* Visualization of the **Kinds** and **Data** associated with other Kinds - such as Instances, Entities and Values.

The Assistant panel can also be used to query a Knowledge Graph using GraphQL \(see below\).

## Workspace Buttons

This is a map of the various options \(as icons\) offered within the Maana KG screen. The activities mentioned in the following pages utilize or mention a number of these icons, so we would suggest that the User take a moment to familiarize themselves with their function and location on the screen.​

\[TBD\]\[NEED IMAGE - Broken on original GitBook.\]

![Example: Assistant Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/image011.png)



![Example: Assistant Panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/image012.png)



