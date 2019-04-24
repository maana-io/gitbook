# Sharing and Reusing Workspaces

## Shared Workspaces

This feature allows you to share your workspace with other Maana users. You can share your workspace _only_ with other users within the same tenant. The other users will be able to edit the workspace and make changes that cannot be reverted. 

### To Share a Workspace:

* Create a Workspace programmatically using the Maana CLI

{% hint style="info" %}
Note: The sharing option via the UI is coming soon!
{% endhint %}

## Workspace Templates

Using Workspace templates can speed up building knowledge solutions as they may come with ready-built Knowledge Graphs, Kinds, Microservices, etc.

### To Create a Workspace Template:

* Navigate to the workspace you would like to turn into a template in the **Workspaces** tab.
* Make sure the workspace name is selected in the Explorer panel.
* Now go to the context panel , and toggle **isTemplate**.

The newly created Workspace Template will appear in the Templates section under the Workspaces tab.

{% hint style="warning" %}
Note: There is currently a known bug that allows you to toggle the isTemplate flag but doesn't implement the functionality. We're working on it and it will be fixed soon!
{% endhint %}

