# RC2-006: Functions using self-recursive types produces an error

{% tabs %}
{% tab title="Description" %}
If a function is recursive, Maana will limit the recursion depth to 8 levels and enforce a 60 second timeout for query execution.
{% endtab %}

{% tab title="Repro Steps" %}
1. Using GraphQL service with the following functions:

dtGetTypeC: C  
dtInputTypeC\(inC: InC\): C

2. Create a function graph called "f2" on a workspace  
dtGetTypeC -&gt; dtInputTypeC -&gt; C

3. In the GraphiQL Panel, select RUN 
{% endtab %}

{% tab title="Expected Results" %}
No errors produced
{% endtab %}

{% tab title="Actual Results" %}
Error:  
"Unexpected token T in JSON at position 0", locations: \[{line: 2, column: 3}\], path: \["f2"\]}
{% endtab %}
{% endtabs %}

