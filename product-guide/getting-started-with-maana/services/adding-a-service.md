# Adding a Service

Is there a service that has Kinds and/or Functions you would like to use, but that doesn't exist yet in Q? This guide will show you how to add it.

## Adding a new service

Navigate to the Services page, scroll down to the Add button and click it.

![Go to the Services page and click the Add button](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Services%20Page%20-%20Add%20Service.png)

You will be presented with a form to enter details about the service.

* **Name**: The name you want to give the service
* **Service Type**: This should be set to GraphQL
* **Endpoint URL**: This should be set to the GraphQL endpoint URL of the service
* **Subscription Endpoint URL**: This is not used
* **Thumbnail URL**: You can change the thumbnail image if you so desire. Enter the URL of the image to use.
* **Tags**: This is not used

![Adding a new service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Adding%20a%20New%20Service.png)

After entering the Endpoint URL, the Test button will become enabled. Clicking this will run an introspection query against the service. If the service is available, the results of the introspection query will be displayed in the Test Results section. If the service is unavailable, an error will be shown in the Test Results section. This can be used to verify that the correct Endpoint URL was entered.

![Example of a failed service test](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Inaccessible%20Service%20Test%20Result.png)

When you are ready, click the Save button to save the service. A snack will be shown in the lower left corner of the screen indicating that the service is being saved.

![Service is being saved](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Saving%20a%20Service%20Snack.png)

Once the service is saved, the snack will change to say it has been saved.

![Service has been saved](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Successfully%20Saved%20Service.png)

{% hint style="info" %}
Saving a service can take some time. The service schema must be introspected and Kinds and Functions created from it. While navigation away from the page is possible while the service is saving, the service and its Kinds and Functions will not be available in Q until the service has finished saving.
{% endhint %}



