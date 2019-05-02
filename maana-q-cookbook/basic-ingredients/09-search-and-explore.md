# Search and Explore

The Knowledge Graph \(KG\) can contain millions of kinds and billions of instances. It is unrealistic to assume a user can, and would want to, work with the entire KG at once. Instead they work with just the parts of the KG related to the problem they are trying to solve or the question they are trying to answer. In v3, users create a Workspace into which they select just the subset of Kinds and Services that they need to build their solution. They use the Knowledge Graph Editor \(KGE\) to select, connect, curate, and populate the graph of kinds and services that form their Workspace.

The user also needs to be able to visualize the instances/entities contained in the kinds and services that comprise their Workspace and to construct more complex queries that allow them to answer questions based on the content of the KG. In deciding how we make these capabilities available to the user through the Knowledge Portal, we need to consider three primary use cases:

* **Preview**: While the user is working in the KGE, they should be able to select \(click/touch\) any kind/service on the canvas and see a summary / preview of the content of whatever is selected. The preview should include visualizations most suited to the display of the **type** and **volume** of content in the selected kind/service \(e.g. bar chart, list, map, etc\). As the user changes the selection from one kind/service to another, this preview should update to reflect the content of the newly selected kind/service. In the preview, the user should be able to interact with the visualizations in order to filter the content, causing the preview visualizations to automatically update. But in this use case, any filtering is restricted to the selected kind/service \(this is equivalent to the v1 summary panel\).
* **Exploration**: Sometimes, a user will want to start from one or more instances/entities of a particular kind and "walk the graph" to understand how that initial selection is connected to other instances/entities in the KG. For example, they might start with a particular Oil Well and want to see which Jobs are associated with that Well. Having isolated the set of Jobs associated with the Well, they want to filter down to a particular type of Job \(e.g. drilling\) and then continue walking the graph to further related concepts such as Drill Strings or Crew Members. At each stage, the user can preview the set of instances/entities and interactively filter them in preparation for walking further in the graph. This use case is an evolution of the v1 "Open Connected" experience and the Airbus Aircog App.
* **Question Answering**: Often users will have specific questions in mind. This can be very simple such as "Which model of Drill Bit is used most frequently", to very complex e.g: "Which Drill Bits does Barry Carlson use most frequently when doing directional drilling through shale in the Gulf of Thailand." or "Which Well Planners have planned the most wells in North America that were completed on time and exceeded production targets." In these cases the user knows what Kind of thing they want in their answer \(Drill Bits or Well Planners\), and they just need to apply filters to the related kinds, resulting in the constraint propagating through the graph. For example they would want to restrict Crew Member to "Barry Carlson", Job Type to "Directional Drilling", Well Location to "Gulf of Thailand" etc and see what Drill Bits remain unfiltered under those constraints.

Although it can be useful to think of these separate use cases, the user will often blend these activities together in the course of working with the KG. For example, when doing **Question Answering**, they use **Preview** to select and filter the related kinds. Also, once they have the answer to the question \(a set of Drill Bits\), the might use **Exploration** to walk the graph to see what else in the graph those Drill Bits are connected to. So it is important that the experiences flow together seamlessly. However, while **Preview** is part of the general KGE experience, **Exploration** and **Question Answering** are about building and editing often complex queries. These queries have a dependency on the KG \(and the KGE in which they are created\), but they are also independent things and need to be managed \(created, saved, viewed, loaded, deleted\) by the user as independent constructs. For example, the user might want to use **Exploration** to look at the connections a particular model of flux capacitor has across the company, then save that and start working on the Barry Carlson Drill Bit question above.

## Design Assumptions / Constraints <a id="UseCase09:SearchandExplore-DesignAssumptions/Constraints"></a>

1. We have very limited time. We are going to do the simplest thing possible to achieve the most important results and get more sophisticated in future. 
2. The Workspace contains the subset of Kinds and Services that the user has chosen to be part of their solution/service. It also contains those Kinds and Services that have been automatically included because they are a dependency of a selected Kind/Service. The kinds and services contained in a Workspace are visible in the Workspace Inventory.
3. A Workspace can contain multiple Knowledge Graphs and multiple Queries
   * Each Knowledge Graph represents a user-configured subset of the Kinds and Services included in the workspace. Users can create, open, edit, close, and delete Knowledge Graphs.
   * Each Query represents a user-configured query \(**Exploration** and **Question Answering** activities\) that depends on the Kinds and Services contained in the Workspace. Users can create, open, edit, close, and delete Queries.
4. The Knowledge Graph Editor \(KGE\) is the editor through which users edit the Knowledge Graphs in their workspace.
5. The Query Editor \(QE\) is the editor through which users edit the Queries in their workspace.
6. There is a Query Panel in the right nav that contains details of the currently open/active Query. This includes a textual description of the query and metadata relating to the query.
7. **Preview** is a feature of both the KGE and QE.

## Stories \(for v3 GA, again keeping it as simple as possible\) <a id="UseCase09:SearchandExplore-Stories(forv3GA,againkeepingitassimpleaspossible)"></a>

As an analyst, I want to...

**PREVIEW**

1. Preview a kind that is on the KGE or QE
   * The user selects \(clicks/touches\) a kind that is on the KGE/QE
   * The preview panel updates to show a set of visualizations depicting the properties of the selected kind
   * The platform chooses 8 properties to visualize and the visualization type that is most appropriate for each
   * OUT OF SCOPE - adding/removing visualization slots, multiple properties on a single visualization
2. Change the properties being visualized and the visualization type being used
   * In the preview panel, the user clicks on the visualization they want to change. They can change the property and the visualization type.
   * OUT OF SCOPE - saving a curated visualization configuration for a kind, adding additional visualization slots
3. Preview content as a table
   * The user can switch the entire preview area into a tabular view of the filtered instances
   * OUT OF SCOPE: custom table configuration
4. Preview content as cards
   * The user can switch the entire preview are into a card view of the filtered instances
   * OUT OF SCOPE: custom card configuration

**EXPLORE / QA \(Query Building\)**

1. Create a Query
   * The user clicks "New Query". This should be presented alongside the "New KG" action.
   * This creates a new Query, adds it to the Workspace, displays it in Explorer with a default name, and opens the new Query in the Query Editor.
   * STRETCH - If the user has a KG active when they click New Query, or has a selection of Kinds on the KGE, the Query should start containing those Kinds.
2. Open a Query
   * Existing Queries are listed in the Workspace Explorer; open them the same way you open KG.
3. Edit a Query
   * With the QE open, the user can start dragging kinds/service from the Workspace Inventory to the QE canvas.
   * Connections between kinds will be displayed but de-emphasized until they are used as part of the Query
   * The user drags ports from one kind to another to define query joins \(including direction\)
   * User can click on the query join lines to define the direction of the query and the distinct/non distinct behavior of the join
   * Preview panel works as normal, 
   * As the user is editing the query, a textual description of the query is displayed in the right nav query panel
   * User can change the query name in the query panel
   * STRETCH: A user should be able to select a Kind on the QE, be able to see on the canvas the other Kinds that are connected to that kind, and be able to easily add one or more to the Query.
4. Save the active query 
   * Maybe they are auto saved?, if not click save in the right nav query panel
5. Close Query
   * Close in the same way you close KG
6. Delete a Query
   * Same way you delete KG
7. STRETCH: Clone a Query
   * From the Workspace Explorer, user can clone a Query

## Building the Query <a id="UseCase09:SearchandExplore-BuildingtheQuery"></a>

Once the user has a Query open in the Query Editor, a query is constructed using three fundamental mechanisms that are repeated to create arbitrarily complex queries:

1. Drag Kinds and Services from the Workspace Inventory onto the QE. In the QE, a Kind/Service can appear on the canvas multiple times. This is to facilitate building queries that use the same kind/service in different contexts.
2. Filtering the instances of a kind based on one or more of its scalar properties \(this is done in preview\)
3. Connecting kinds together to describe how the filters propagate across the graph as left outer joins. This is done by clicking the connections that exist between kinds and including them as part of the Query. 

As the user performs these actions building up increasingly sophisticated queries, the right nav query panel updates to display a textual description of the query. And allows the user to manage the lifecycle / metadata of the query.

Using these three simple mechanism, the user can achieve both **Exploration** and **Question Answering** use cases, as well as complex queries that blend the approaches simply by deciding the order and direction of their filtering and joining. An example of the high level flow is described next.

## Flow <a id="UseCase09:SearchandExplore-Flow"></a>

The user is working with a Knowledge Graph in the KGE. They want to answer the question "Which Drill Bits does Barry Carlson use most frequently when doing directional drilling in the Gulf of Thailand".

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996919/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20010.pdf?version=1&modificationDate=1519203658457&api=v2) PDF

Drill Bits is currently selective and is visualized in Preview. The user clicks "New Query".

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996920/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20020.pdf?version=1&modificationDate=1519203658592&api=v2) PDF

A new Query is created and displayed in the Query Editor. The Kind selected \(Drill Bit\) when the Query was created is included in the new Query. Explorer updates and the right nav switches to a Query Panel showing details of the current Query. This includes a textual description of the query being created \(represented in the following diagrams in a placeholder pseudo-query syntax\).

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996921/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20030.pdf?version=1&modificationDate=1519203658669&api=v2) PDF

The user drags the Job Kind from the Inventory onto the QE

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996922/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20040.pdf?version=1&modificationDate=1519203658771&api=v2) PDF

When Job is dropped on the QE, it receives the focus so is visualized in preview, and it is connected to Drill Bit as it is in the KG. The query panel updates

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996923/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20050.pdf?version=1&modificationDate=1519203658844&api=v2) PDF

The user drags Job Type from the Inventory and drops it on the QE. They want to be able to filter down to "Directional Drilling" jobs.

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996924/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20060.pdf?version=1&modificationDate=1519203658922&api=v2) PDF

Job Type is connected to Job as it is in the KG. Preview and Query Panel updates to reflect the addition of Job Type

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996925/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20070.pdf?version=1&modificationDate=1519203659061&api=v2) PDF

But, currently, the QE shows Job pointing at Job Type, but the user wants to constrain the set of Jobs by a particular job type. So they select the connection and reverse the direction of the arrow. This only affects the query logic, not the KG.

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996926/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20080.pdf?version=1&modificationDate=1519203659227&api=v2) PDF

Now the user uses the visualizations in Preview to filter the Job Type. Which propagates to Job, filtering to only those Jobs of type Directional Drilling, which in turn propagates to Drill Bit leaving only those Drill Bits used in Directional Drilling Jobs.

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996927/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20090.pdf?version=1&modificationDate=1519203659378&api=v2) PDF

Using the same process, the user adds Crew Member \(filters to Barry Carlson\) and Location \(filters to Gulf of Thailand\) to the Query. Note that Location is a few hops away from the Drill Bit, so the intervening Kinds are added as minimized Kinds. The user can expand them if they want. The overall result is a query that constrains Drill Bits to just the set used by Barry Carslon, on Directional Drilling Jobs, on Wells that are in the Gulf of Thailand.

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996935/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20100.pdf?version=1&modificationDate=1519205214653&api=v2) PDF

Happy with the Query, the user changes its name.

[![](https://confluence.corp.maana.io/rest/documentConversion/latest/conversion/thumbnail/36996936/1)](https://confluence.corp.maana.io/download/attachments/36995864/2017.11.27%20KGE%20UX%20110.pdf?version=1&modificationDate=1519205214734&api=v2) PDF

