# RC1-025: QueryGraph: cannot delete a link between kinds

{% tabs %}
{% tab title="Description" %}
Can you delete a link on QueryGraph?
{% endtab %}

{% tab title="Repro Steps" %}
1. Create 2 kinds on knowledge graph.
2. Create a query graph for these 2 kinds.
3. Draw a link between 2 links on QueryGraph.
4. Click on the link and try to delete the link \(Issue 1: no button to delete link on QueryGraph\).
5. If I click on the "Remove from Workspace" button, it will give error \(Issue 2\).
{% endtab %}

{% tab title="Expected Result" %}
Have a button to delete link on QueryGraph.
{% endtab %}

{% tab title="Actual Result" %}
Issue 1: No button to delete a link on QueryGraph.

Issue 2: Use "Remove from Workspace" to delete link on QueryGraph will give error:

ApolloError.js:58 Uncaught \(in promise\) Error: GraphQL error: Cannot read property 'map' of null  
at new t \(ApolloError.js:58\)  
at Object.next \(QueryManager.js:355\)  
at y \(Observable.js:152\)  
at b \(Observable.js:196\)  
at e.value \(Observable.js:248\)  
at y \(Observable.js:152\)  
at b \(Observable.js:196\)  
at e.value \(Observable.js:248\)  
at httpLink.js:173
{% endtab %}

{% tab title="Work-around Solution" %}
The work-around is to remove the kind from one side of the connection you want to remove from the graph, and then re-add it to the graph.
{% endtab %}
{% endtabs %}



