# What's New in 3.2.1

## Assistant API

Assistants now have an official API complete with a sample project for getting started creating Assistants quickly. You can find the sample project here: [https://github.com/maana-io/q-assistant-client](https://github.com/maana-io/q-assistant-client)

The Assistant API allows interacting with a Workspace and the entities within the Workspace, providing the ability for custom UIs to be created that can extend the functionality provided by Q. Some of the things it allows include adding, deleting, or modifying Kinds and Functions; listening for changes made to the Workspace; and accessing details about entities within the Workspace. 

## Lambda Assistant and Service

The [Lambda Assistant](../catalog/assistants/lambda.md) and backing service allows code snippets to be attached to Q functions instead of needing to write full-blown microservices.  This is often convenient for returning constants, _projectors_ and _constructors_, transformations, calculations, etc.

![The Lambda Assistant allows writing a Function implementation in JavaScript](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/lambda_assistant.gif)

## Lesson Assistant and Service

## Snap to Grid

The UI now supports toggling snap to grid for nodes. When turned on nodes will stay aligned with the grid lines. The grid lines now also move when panning and zooming!

![Turn on snap to grid](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/snap_to_grid.gif)

## Reset Graph Zoom

Do you ever wish you could "go back" to the default zoom level? Well now you can with a simple mouse click!

![Reset the zoom level to the default](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/reset_graph_zoom.gif)

## Function Nodes

There are a few changes made to bring Functions in parity with Kinds in the Knowledge Graph. When the type of argument or output in a Function node is set to a Kind, the link to the Kind is now shown just like with Kind nodes.

![Function nodes display links to Kinds](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/function_node_links.png)

You can also hover over the argument or output type of a Function to see a preview of the Kind. Clicking on the argument or output type will add the Kind to the Knowledge Graph. This is the same behavior as Kinds.

![Preview and add Kind referenced by a Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/click_to_add_kind_function.gif)

## Graph Performance Improvements

There was a focus this release to make the graph extra snappy. As part of this, a whole new layout algorithm was developed that makes adding nodes to the graph faster and layout more consistent.

All interactions with the graph \(panning, zooming, dragging nodes, entering and exiting edit mode\) are considerably faster and smoother. These performance improvements are especially noticeable on graphs with lots of nodes.

Finally, anything that adds a node to the graph is much faster. This includes creating Kinds or Functions, duplicating nodes, or dragging and dropping from search or the Explorer or Inventory panels.

## Component Version Export

There is now an export button on the System Information page. This downloads all of the installed components and their versions in a CSV.

![Export component versions as a CSV](https://maanaimages.blob.core.windows.net/maana-q-documentation/What%27s%20New%203.2.1/component_version_export.gif)

## New CLI Templates

Use the Maana Q CLI's `mdeploy` command to bootstrap a Knowledge Service, Bot, or Application.

### React \(JavaScript\) Knowledge Assistant \(Basic\)

### React \(JavaScript\) Knowledge Assistant \(Advanced\)

### React \(JavaScript\) Knowledge Application

## New Training Material

To help you get started or advance your skills in becoming productive with Q, we have completely revamped our [training material](../training/introduction.md), in conjunction with the new Lesson Assistant.

## The Rest

As always, there are lots of bug fixes and improvements - notably faster Search and more robust Workspace cloning - included in this release.

