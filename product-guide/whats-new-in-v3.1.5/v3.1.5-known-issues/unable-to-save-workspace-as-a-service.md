# RC1-015: Unable to save workspace as a service

{% tabs %}
{% tab title="Description" %}
Unable to save workspace as a service.
{% endtab %}

{% tab title="Repro Steps" %}
1. Create workspace.
2. Open info panel of workspace and copy "Workspace Service URL" field.
3. Open Admin page.
4. Create service based on copied service URL.
{% endtab %}

{% tab title="Expected Result" %}
A service is created.
{% endtab %}

{% tab title="Actual Result" %}
UI:

```
Failed to save the service: GraphQL error: Error/s in apollo-link operation: [{"message":"Response not successful: Received status code 401","locations":[{"line":2,"column":3}],"path":["addService"]}]

```
{% endtab %}
{% endtabs %}



