# RC2-001: Implement pagination fetching for Kind previews

{% tabs %}
{% tab title="Description" %}
When changing the type of a field of a Kind \(this can be done through the context panel or through the in-node editing experience\), the Kind preview will not correctly display the data in the column representing the field \(the data will disappear\) until you unselect the Kind and selects it again. 

Also, there may be certain cases where adding or removing a field does not get reflected in the Kind preview window until you unselect the Kind and selects it again.
{% endtab %}

{% tab title="Work-around" %}
Implementing pagination fetching for the results shown in the preview pane when selecting a Kind will reduce the likelihood of a browser OOM error and dramatically improve UI performance when a Kind is selected.

Only the results needed for the current page in the preview panel need to be queried. When you page through the results, more should be fetched dynamically.
{% endtab %}
{% endtabs %}



