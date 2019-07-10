# Deleting a Kind via CLI

{% hint style="info" %}
When deleting a kind via CLI without knowing the dependency graph, it may be difficult to find and replace all previous references to the old kind with a new kind if that was the intention. 

It is recommended to not delete kinds without knowing the implications. Down-casting to string is a fail-safe to not kill all dependencies.
{% endhint %}



