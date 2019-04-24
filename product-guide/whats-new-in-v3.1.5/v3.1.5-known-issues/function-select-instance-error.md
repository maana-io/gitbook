---
description: >-
  Q function "select instance": give error " Cannot read property 'kinds' of
  undefined".
---

# RC1-021: Function "select instance" error

{% tabs %}
{% tab title="Description" %}
Error using function.
{% endtab %}

{% tab title="Repro Steps" %}
1. Given a workspace "myFun" has a few valid functions.
2. Use the service in a new workspace "New Workspace".
3. Pull function "fun3" which uses input argument of type Kind of service "lcsvc6: BookIdNotDefInput" onto knowledge graph.
4. Try to run the function in the "New Workspace".

ISSUES:

1. "KIND" is displayed, it should be "lcsvc6:BookIdNotDefInput".
2. "Select Instance" when Run give error.
{% endtab %}

{% tab title="Expected Result" %}
Be able to run the function from another workspace and "select instance".
{% endtab %}

{% tab title="Actual Result" %}
Not able to use "select instance".  
Error is given:"Cannot read property 'kinds' of undefined".
{% endtab %}
{% endtabs %}

