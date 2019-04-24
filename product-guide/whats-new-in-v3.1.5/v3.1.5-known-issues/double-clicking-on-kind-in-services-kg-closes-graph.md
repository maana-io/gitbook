# RC1-009: Double clicking on kind in service's KG closes graph

{% tabs %}
{% tab title="Description" %}
Double clicking on a kind should have consistent behavior. Double clicking on a blue \(system kind?\) rectangle causes the associated service's knowledge graph to close.  
{% endtab %}

{% tab title="Repro Steps" %}
1. Open a new workbook.
2. Select any service from the inventory \(e.g. physical quantity\).
3. Double click on any of the blue rectangles that appear on the canvas.
{% endtab %}

{% tab title="Expected Result" %}
The context panel should show information about the selected kind.
{% endtab %}

{% tab title="Actual Result" %}
The knowledge graph for the service closes and replaced with the workspace's knowledge graph.
{% endtab %}
{% endtabs %}

