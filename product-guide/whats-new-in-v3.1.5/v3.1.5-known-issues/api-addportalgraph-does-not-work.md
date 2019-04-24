# RC1-007: API "addPortalGraph" does not work

{% tabs %}
{% tab title="Description" %}
Given "addPortalGraph" does not work.  Use "addPortalGraphs" as a temporary solution to run QA test cases.
{% endtab %}

{% tab title="Repro Steps" %}
From QA regression test, this mutation used to work with all valid args:

```text
mutation addFunctionGraph(
  $wsId: ID!
  $name: String!
  $functionId: ID!
) {
  addPortalGraph(
    input: { workspaceId: $wsId, name: $name, id: $functionId, type: FUNCTION }
  ) {
    id
    name
    function {
      id
    }
  }
}

```

The schema is:

```text
addPortalGraph(input: AddPortalGraphInput!): PortalGraph
```
{% endtab %}

{% tab title="Expected Result" %}
No error.
{% endtab %}

{% tab title="Actual Result" %}
"message": "Adding a PortalGraph of type Function to a Workspace is not allowed."
{% endtab %}
{% endtabs %}

