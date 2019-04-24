# RC1-024: Kinds imported to WS: no boilerplate functions for adding instances

{% tabs %}
{% tab title="Description" %}
Want to add data for kinds that have been imported from the external service. Do not have an option except KindDB API. 
{% endtab %}

{% tab title="Repro Steps" %}
1. Create workspace and import service [https://maana-distance.herokuapp.com](https://maana-distance.herokuapp.com/).
2. Create a kind with fields named "NewKind".
3. Import created workspace to another workspace.
{% endtab %}

{% tab title="Expected Result" %}
There are not only addNewKinds methods, but for kinds that were imported from the services as well. 
{% endtab %}

{% tab title="Actual Result" %}
Only bolierplates functions for manually created kinds. 
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Note: 

* Boilerplate is generated not for 'workspace' kinds, but for 'model service' kinds. Creating new workspace creates two service - logic \(to store workspace's designed functions\) and model \(to store workspace's kinds\).
* Importing kind from other service onto workspace doesn't add it to model service - it 'imports' or 'uses' it - so no boilerplate will be generated.
* Importing functions onto workspace will not expose them in CKG/logic service either - they belong to other service.  **This** will change when Service Imports and Service Exports are implemented - user will be able to import a function from other service and reexport it. Types \(Kinds\) will be exported only based on functions where they are used.
{% endhint %}

