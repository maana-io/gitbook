# RC2-003: UI should support displaying partial results of evaluation

\[TBD\] @Andrey

{% tabs %}
{% tab title="Description" %}
There was an issue in PQ service where one of the resolvers would return a failure, and this raised very interesting point:

* GraphQL supports partial results. So it is perfectly valid situation where you have response that contains both 'data' and 'errors' parts. Maana doesn't show partial results.
* As GraphQL services are built, you must show actual GraphQL response - with errors, data, tracing etc - limiting you to only see part of the response is not really a good way to 'build graphql services'. Having errors in response will remove the broken logic of a snack that will show just part of the error.
{% endtab %}

{% tab title="Repro Steps" %}
1. Open a new workbook
2. Add the physical quantity service to the inventory panel
3. Expand the physical quantity service in the inventory panel
4. Select the "parse" function from the physical quantity service.
5. Select the run in the context panel
6. Execute with the following inputs:

      - source: "10 m"

      - systemInputs: null

      - dimensionInputs: null
{% endtab %}

{% tab title="Expected Result" %}
The assistant panel will display the result of the graphQL query.
{% endtab %}

{% tab title="Actual Result" %}
An error box pops up with the following message:

"Unable to execute function: Cannot return null for non-nullable field UnitOfMeasurePrefix.id."
{% endtab %}
{% endtabs %}

