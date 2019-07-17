# Using Kinds and Functions from services

Eventually, when building a solution you will need to use Kinds and Functions from services in the Functions you created. \(see [Services](./#the-importance-of-reusing-kinds-and-functions) for reasons why\)

## Building a solution with Kinds and Functions from a service

In order to use Kinds and Functions from a service they first need to be added to the Workspace. There are two ways this can be accomplished: by adding the service containing the Kinds and Functions to the Workspace or adding specific Kinds and Functions to the Workspace.

### Adding a service to the Workspace

If you are unsure exactly what Kinds and Functions you want to use, but you have an idea of the service \(or services\) that contains them, you can add the service to the Workspace inventory and look through the Kinds and Functions it has.

To add a service to the Workspace inventory, the first step is to search for it.

![Example search for the Maana Entity Extractor service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Example%20Service%20Search.png)

Once you find the service you are looking for, drag it from the search results and drop it into the Workspace inventory.

{% hint style="info" %}
When dragging and dropping items, the drop area will change to have a blue shaded background when the drop is allowed.
{% endhint %}

Once dropped, expand **Services -&gt; GraphQL** in the inventory and you should see the service listed there. Expand the service to see all of the Kinds and Functions available within it.

![The Maana Entity Extractor service has been added to the Workspace inventory](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Service%20Added%20to%20Inventory.png)

Any of the Kinds and Functions listed in the inventory can be dragged and dropped into the Canvas area of the Workspace to add the Kind or Function to the currently displayed graph.

### Adding a Kind or Function to a Workspace

If you know the name of the Kind or Function you are looking for and want to directly add it without first adding a service, it can be dragged and dropped into the current graph.

First, search for the Kind or Function by name.

![Search for the Person Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Search%20for%20Person%20Kind.png)

When you have found the Kind you are looking for, drag and drop it into the Canvas area of the Workspace. This will add it to the currently displayed graph _and_ it will be available in the Workspace inventory.

![The Person Kind from Maana Entity Extractor has been added to the current graph](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Person%20Kind%20Added%20to%20Graph.png)

![The Person Kind from Maana Entity Extractor is also available in the Workspace inventory](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Person%20Kind%20Added%20to%20Inventory.png)

Once a Kind has been added to the Workspace, it is available for selection when choosing types for fields of Kinds and Functions.

![The Person Kind from Maana Entity Extractor is now available as a field type in Functions](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Imported%20Kind%20is%20Available%20for%20Field%20Type.png)

{% hint style="info" %}
Most things within a Workspace that rely on Kinds or Functions require that the Kind or Function be in the Workspace inventory in order to be available. For example, only Kinds that exist in the Workspace inventory are available for selection in the type drop-down of fields when editing Kinds and Functions. If a specific Kind or Function is missing from something, make sure it is available in the Workspace inventory. It probably just needs to be added to the Workspace.
{% endhint %}

