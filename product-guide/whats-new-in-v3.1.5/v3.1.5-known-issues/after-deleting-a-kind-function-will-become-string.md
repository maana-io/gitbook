# RC1-023: After deleting a kind, function will become "String"

{% tabs %}
{% tab title="Description" %}
What to display when "kk1" kind has been deleted from workspace?
{% endtab %}

{% tab title="Repro Steps" %}
1. Create a workspace.
2. Create a kind called "kk1" with at least one field.
3. Create a function "fun1" that output of type "kk1".
4. Click on "kk1" node on knowledge graph, click "delete" garbage can on left panel.
5. Refresh workspace.
6. Look at the "fun1" node on knowledge graph, the output type is "STRING" &lt;-- Issue 1.
7. Double click on the node to edit.
8. The output type is empty &lt;-- Issue 2.
{% endtab %}

{% tab title="Expected Result" %}
Is it possible to mark the output type of the missing "kk1" kind in Red empty string?
{% endtab %}

{% tab title="Actual Result" %}
* Issue 1: It changed to "STRING" when it cannot find "kk1" deleted kind.
* Issue 2: When editing, the "STRING" is gone and becomes empty string
{% endtab %}

{% tab title="Resolved" %}
Issue has been resolved.  

{% hint style="info" %}
If you experience this issue while working in Maana Q, please file a [bug report](https://maana-ue.gitbook.io/product/reference-docs/report-bugs).
{% endhint %}
{% endtab %}
{% endtabs %}

