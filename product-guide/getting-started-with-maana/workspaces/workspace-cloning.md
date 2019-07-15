# Cloning a Workspace

Let's say that there is a particular Workspace that you would like to use as a starting point for a new solution. How can you do this? Why, with Workspace cloning, of course!

Workspace cloning gives you the ability to

* Try out different solutions to a problem. The solutions can be modified independently of one another and compared for performance, accuracy, etc.
* Reuse Workspace templates as a starting point for new solutions

Let's say that you have an idea for an even cooler Workspace but you want to use the Workspace you created before as a starting point. First, find the Workspace on the Workspaces page under My Workspaces and click the clone button

![Click the clone button to clone a Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/My%20Workspaces%20Cloning.png)

The Workspace will take a few seconds to clone during which you will see the cloning indicator.

![Cloning in progress](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Cloning%20In%20Progress.png)

The new workspace has copies of all of the Kinds, Functions, and Knowledge Graphs that were created in the original Workspace.

![The new Workspace, cloned from the original!](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Cloned%20Workspace.png)

You are now free to edit the Workspace without affecting the original.

![The cloned Workspace has been renamed to &quot;My Even Cooler Workspace&quot; ](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Renamed%20Cloned%20Workspace.png)

Any Public Workspace can also be cloned.

![Cloning a public Workspace](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Cloning%20a%20Public%20Workspace.png)

Workspace Templates have cloning \(instead of opening\) as the default action. Simply click on a Workspace template and it will clone it.

![Cloning a Workspace template](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Cloning%20a%20Workspace%20Template.png)

## How does cloning work?

Cloning copies the Kinds, Functions, and Knowledge Graphs that were created in the original Workspace. Any references to these Kinds and Functions in the original Workspace will be updated to refer to the copies created in the new Workspace. References to Kinds and Functions imported from services will have the references copied to the new Workspace. 

Let's look at an example of what this would mean. In the picture below, KindA and functionB are both created in the current Workspace and will be copied when the Workspace is cloned. The "extract" Function is imported from the "Maana Named Entity Recognition" service. The new Workspace will reference the same "extract" Function instead of creating a copy of it.

![The &quot;extract&quot; Function is imported from the &quot;Maana Named Entity Recognition&quot; service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Workspace%20with%20external%20Function.png)

Instances of Kinds \(including Files and Documents created within the Workspace\) are not copied when cloning a Workspace. However, references to Instances will be copied. This means the new Workspace will refer to the same Instances that the original Workspace referred to.

Services that were in the original Workspace's Inventory will be in the new Workspace's Inventory as well. The new Workspace should look the same as the original with the possibility of a few differences due to Instances being referenced instead of copied.

{% hint style="info" %}
The time it takes to clone a Workspace is dependent on how complex the Workspace is.
{% endhint %}



