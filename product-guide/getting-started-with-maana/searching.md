# Searching

Search plays a prominent role in Q. It is the only way to perform certain actions in the UI. Let's take a look at how search works.

## Performing a Search

Searching is done in the search bar located at the top of the page. Most actions taken involving search occur within the context of a Workspace.

![The search bar](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Search%20-%20Main.png)

When performing a search you will notice categorization among the results. Each category has specific uses.

![Example search results](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Search%20Results%20-%20Workspace.png)

Let's break down each category.

{% hint style="info" %}
If a category is not selectable, it does not have results.
{% endhint %}

### Kinds

The Kinds category \(along with Functions\) is one of the most commonly used categories in the search results. This category contains all the Kinds matching the search. These can be added to a Knowledge Graph or Function Graph through drag and drop. Click and drag the search result to the canvas. 

![Dragging a search result to the Canvas](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Drag%20and%20Drop%20Kind%20from%20Search.png)

{% hint style="info" %}
The Kind results are displayed as "&lt;service name&gt;: Kind: &lt;kind name&gt;". In the example above, the search result that was dragged indicates that it is the Kind named "Workspace" from the service named "Maana Azure Crawler". System Kinds do not have a service.
{% endhint %}

The blue background indicates a valid drop. Dropping the Kind will add it to the Knowledge Graph and the Workspace \(if it already isn't a part of the Workspace\).

![The Workspace Kind from Maana Azure Crawler has been added to the Knowledge Graph](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Kind%20Added%20to%20Knowledge%20Graph.png)

### Functions

The Function category contains all of the Functions matching the search. It looks and behaves in a similar manner to Kinds. Functions can be dragged and dropped to the Canvas area to add them to a Knowledge Graph or Function Graph and to the Workspace \(if it hasn't already been added\).

![Example Function search results](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Search%20Results%20-%20Functions.png)

{% hint style="info" %}
Function search results are shown in the form "&lt;service name&gt;: &lt;function name&gt;"
{% endhint %}

### Workspaces

The Workspaces category has all of the Workspaces matching the search. \(see a pattern here?\) What can you do with these? They can be dragged and dropped onto the Workspaces ribbon to open the associated Workspace.

![Dragging and dropping a Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Dragging%20and%20Dropping%20a%20Workspace.png)

### Knowledge Graphs

Knowledge Graphs can be dragged and dropped from the Knowledge Graphs category into the Explorer panel. This will create a new Knowledge Graph in the Workspace with the same name as the one that was dropped. The new Knowledge Graph will contain references to everything that was in the original Knowledge Graph.

![Dragging a Knowledge Graph to the Explorer panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Dragging%20Knowledge%20Graph%20to%20Explorer%20Panel.png)

{% hint style="info" %}
Knowledge Graph search results are in the form "&lt;workspace name&gt;: &lt;knowledge graph name&gt;"
{% endhint %}

### Queries

The Queries category contains Query Graphs. They can be dragged and dropped into the Explorer Panel just like a Knowledge Graph.

{% hint style="info" %}
Query Graphs are deprecated in 3.2.0. You can still search for existing ones but the ability to create new ones has been removed.
{% endhint %}

### Services

The Services category contains service search results. Service search results can be dragged and dropped into the Inventory panel of the Workspace. The service and all of its Kinds and Functions will display there for easy access when creating solutions in the Workspace.

![Dragging a service to the Inventory](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Dragging%20Service%20to%20Inventory.png)

![Service added to the Inventory with all of its Kinds and Functions shown](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Dropped%20Service%20to%20Inventory.png)

### Instances

The final category is Instances. This contains everything that doesn't fit into one of the other categories. It includes anything that is an Instance of a Kind that matches the search, including Files and Documents.

![Example Instance search results](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Instance%20Search%20Results.png)

Instances can be dragged and dropped onto a Knowledge Graph to add the Instance to the Knowledge Graph and the Workspace \(if it doesn't already exist\).

{% hint style="info" %}
Instance search results are displayed in the form "&lt;service name&gt;: &lt;Kind name&gt;: &lt;Instance name&gt;"
{% endhint %}





