# RC2-004: Using auto-generated kinds as field types is not supported

{% tabs %}
{% tab title="Description" %}
* You create kind K1 in the workspace and adds field f1: String
* You create kind K2 in the workspace and adds fields f1: String and f2: AddK1Input \(kind that is automatically generated in workspace inventory upon creation of K1\)
{% endtab %}

{% tab title="Actual Result" %}
* Opening Workspace Service in GraphIQL will not expose KindDB Model and CKGErrors resolver will produce error that looks like:

  ```text
  {
    "data": {
      "CKGErrors": [
        "Error while introspecting KindDB Model schema: [{\"message\":\"Error: Failed to find type for field: { id: '3d22970f-52a9-406f-85be-56f2ce51091d',\\n  name: 's',\\n  description: '',\\n  type: 'KIND',\\n  typeKindId: 'd85524db-feb2-4d68-8b7d-26140e8a8f74:d6810698-da84-4e52-9bab-c976bcf4369a:addinput',\\n  modifiers: [],\\n  kind: null,\\n  hide: false,\\n  autoFocus: false,\\n  displayAs: [],\\n  readonly: false,\\n  isDeleted: false }\"}]"
      ]
    }
  }
  ```
{% endtab %}

{% tab title="Solutions" %}
Using auto-generated kinds as kind fields is not supported. There are two solutions:

* If this has been done by mistake, you can edit a kind and change the type of the field, or remove the field, and KindDB Model will be functional again
* If the shape of auto-generated kind is needed, you should create a kind of the same shape manually, as "duct-taping" will allow coercing the types as long as they have the same structure.
{% endtab %}
{% endtabs %}

