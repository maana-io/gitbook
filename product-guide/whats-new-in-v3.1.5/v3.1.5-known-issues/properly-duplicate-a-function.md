# RC1-004: Properly duplicate a function

{% tabs %}
{% tab title="Description" %}
The duplicate functionality was never created for functions.
{% endtab %}

{% tab title="Repro Steps" %}
1. Add a function to the graph.
2. Make sure it is selected.
3. Then duplicate it.
{% endtab %}

{% tab title="Expected Result" %}
Expected results are to make a duplicate of the function and its arguments, and create a new function graph for it if it's a CKG function with an empty implementation.
{% endtab %}

{% tab title="Actual Result" %}
What actually happens is that it makes a copy of the function instance, but does not change anything else.

{% hint style="warning" %}
**Known limitation** - When a function is duplicated on the UI it will contain no implementation, like with duplication of a kind, and will not duplicate its contents \(data\).
{% endhint %}
{% endtab %}
{% endtabs %}

