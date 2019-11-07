# RC1-003: CKGErrors after function removing

{% tabs %}
{% tab title="Description" %}
There are CKGErrors after removing function. Refreshing the page doesn't help. Error still presented.
{% endtab %}

{% tab title="Repro Steps" %}
1. Create workspace.
2. Add function to the workspace with any fields.
3. Remove it using delete button.
{% endtab %}

{% tab title="Expected Result" %}
Function removed from the explorer, inventory and related function graph also removed, there is no errors in CKGErrors.
{% endtab %}

{% tab title="Actual Result" %}
Function removed, but CKGErrors return error:

```python
{
  "data": {
    "CKGErrors": [
      "Error while introspecting ckgSchema: {\"name\":\"ServerError\",\"response\":{\"size\":0,\"timeout\":0},\"statusCode\":400,\"result\":{\"errors\":[{\"message\":\"CKGError: Failure fetching functions of service fc62d705-d4da-4e0a-a6cc-a66647386caf: [Cannot return null for non-nullable field Function.arguments.]\"}]}}"
    ]
  }
} 
```
{% endtab %}

{% tab title="Resolved" %}
Issue has been resolved.  

{% hint style="info" %}
If you experience this issue while working in Maana Q, please file a [bug report](https://maana-ue.gitbook.io/product/reference-docs/report-bugs).
{% endhint %}
{% endtab %}
{% endtabs %}

