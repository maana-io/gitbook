---
description: A journey of a thousand miles begins with a single step
---

# Creating Your First Service

## **Step-by-Step Instructions**

**Step 1.** Create a new [Workspace](../../../product-guide/getting-started-with-maana/workspaces/#what-is-a-workspace) from the dashboard or the Workspaces tab bar

Workspace are where you design a sub-graph within the CKG.  These take the form of **live** cloud-based \(or on-prem\) GraphQL-based microservices.  You can think of them like "projects" and are often used just to _sketch_ out different design ideas.

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 2.** Rename the Workspace to `<your name> Hello World`in the Info Context panel

The portal Workspace user interface consists of various _panels_, such as:

* **Explorer**: a [Knowledge Graph](../../../product-guide/reference-guide/technical-design-and-architecture/kinds-and-fields/) and [Function Graph](../../../product-guide/reference-guide/technical-design-and-architecture/function-modeling/) browser
* **Inventory**: everything available within your Workspace, organized by type; think of this as your _palette_
* **Canvas**: where you create and manage graphs
* **Assistants**: plug-ins that provide custom interactions for authoring, visualization, interaction, diagnostics
* **Context**: deeper interactions \(e.g., edit settings, run functions\) with the currently focused item, such as the Workspace itself, Kinds, Functions, services

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 3.** Save the Workspace settings

Changing information in the context panel requires an explicit **Save**, while general Workspace operations \(e.g., creating graphs, Kinds, Functions\) do not.

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 4.** Select the default `New Knowledge Graph`

A Workspace can contain multiple Knowledge Graphs.  They are simply views on the Kinds, Functions, and instances from the inventory.  There is only a single copy of any element within the workspace and all elements must have unique names.

{% hint style="info" %}
Kinds and Functions must have **unique names** within a Workspace
{% endhint %}

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 5.** Create a new Function



[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step2.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step2.gif)

\*\*\*\*

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 6.** Name the Function, `sayHello`

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step3.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step3.gif)

\*\*\*\*

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 7.** In the Function node, create a Field called `input` of type `STRING` and click save

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step4.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step4.gif)

\*\*\*\*

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

**Step 8.** Expand the `sayHello` Function

_Expanding_ a Function means to edit its **composition**. 

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

9. Search for the `Greetings` Service and drag-and-drop it to Workspace Inventory.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step5.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step5.gif)

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

10. Expand "Greetings" in Inventory to locate the "helloWorld" function. Drag and drop "helloWorld" from Inventory to the Canvas. Wire input and output. sayHello function is now complete.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step6.mov) 

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step6.gif)

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

7. To test the functionality we just created, locate sayHello function in the Explorer panel and hit Run in the Context Panel . Provide an input. In the Assistant Panel, we see the result.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step7.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step7.gif)

{% hint style="warning" %}
**TODO: screenshot**
{% endhint %}

