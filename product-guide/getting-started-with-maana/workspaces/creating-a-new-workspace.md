# Creating a New Workspace

## Create a New Workspace

As mentioned earlier, your Workspace is the key to utilizing the Computational Knowledge Graph \(CKG\) and unlocking the power of the Artificial Intelligence \(AI\) data stream.  If you are not using an existing Workspace, you will want to create one of your own.  This can be done in a few steps.

* Select the **Workspaces** tab at the top of the Maana portal,
* Select the "New Workspace" button ![](../../../.gitbook/assets/screen-shot-2019-07-10-at-1.23.01-pm.png) on the left side of the Workspaces ribbon

![Workspace Ribbon](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspaces%20Ribbon.png)

Once the Workspace is finished being created, you will be taken to the Workspace screen. Initially it will be empty except for a single Knowledge Graph.

![Starting view of a new Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Closing%20a%20Workspace.png)

{% hint style="info" %}
To close the currently open Workspace, select the close button located on right side of the Workspaces ribbon. This does not delete the Workspace; it simply removes it from the Workspaces ribbon.
{% endhint %}

Notice the name is **New Workspace**. Let's change it to **My Really Cool Workspace**.

First, select the Workspace name in the Explorer panel. Once it is selected, the information about the Workspace will be available in the Context panel's Information pane.

![Screen showing the Workspace details in the Information pane of the Context panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspace%20Selected%20in%20Explorer%20Panel.png)

Inside of the Information pane, you can see the details of the Workspace as well as change the name, thumbnail image, whether it is public, and whether it is a template. We'll talk more about the isPublic and isTemplate options are later. For now, let's enter our new name and save it.

![Update the Workspace name and click Save](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Renaming%20Workspace.png)

Once the Workspace is saved, you will notice that the name has been updated in the Explorer panel and the Workspace ribbon.

![The name has been updated to My Really Cool Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspace%20Renamed.png)

When you create a Workspace, a GraphQL service \(of the same name as the Workspace\) is created that backs the Workspace. You can interact with that service using the GraphQL IDE Assistant in the Workspace.

![Workspace with the GraphQL IDE Assistant](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/GraphQL%20IDE%20Assistant.png)

This allows you to introspect the GraphQL schema for the service backing the Workspace to see what types, queries, and mutations are available. It also allows executing queries or mutations against the service.

## My Workspaces

Once a workspace is created, it will appear in the **My Workspaces** area of the **Workspaces Tab**.

![The new Workspace showing up under My Workspaces](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/My%20Workspaces%20with%20New%20Workspace.png)

{% hint style="info" %}
If you change the thumbnail image of a Workspace, the new thumbnail image would be shown here. Currently, only images accessible via URL are supported.
{% endhint %}

