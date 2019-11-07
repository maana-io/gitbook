# RC2-005: GraphQL Query using "AND" to join 2 kinds produces duplicate instance rows

{% tabs %}
{% tab title="Description" %}
Joining two data sets in a GraphQL query on a common field may return duplicate rows:

\*Given only two rows in each file:  
**Schools\_small\_stateIN\_.csv**  
schoolID,name\_full,city,state,country  
evansville,University of Evansville,Evansville,IN,USA  
butler,Butler University,Indianapolis,IN,USA

**Parks\_small\_stateIN\_.csv**  
park.key,name,park.alias,city,state,country  
IND01,South Street Park,,Indianapolis,IN,US  
IND02,Seventh Street Park I,,Indianapolis,IN,US

Joining on "state" field from Schools to Parks as inner join yields:

**Step 1: \(join\)**  
evansville,University of Evansville,Evansville,IN,USA &lt;- join -&gt; IND01,South Street Park,,Indianapolis,IN,US  
evansville,University of Evansville,Evansville,IN,USA &lt;- join -&gt; IND02,Seventh Street Park I,,Indianapolis,IN,US  
butler,Butler University,Indianapolis,IN,USA &lt;- join -&gt; IND01,South Street Park,,Indianapolis,IN,US  
butler,Butler University,Indianapolis,IN,USA &lt;- join -&gt; IND02,Seventh Street Park I,,Indianapolis,IN,US

**Step 2: \(projection\) \[regardless of ordering\]**  
IND01,South Street Park,,Indianapolis,IN,US  
IND02,Seventh Street Park I,,Indianapolis,IN,US  
IND01,South Street Park,,Indianapolis,IN,US  
IND02,Seventh Street Park I,,Indianapolis,IN,US

Suggest the use of "distinct" clause in the query to eliminate the duplicates and return only two parks.
{% endtab %}

{% tab title="Repro Steps" %}
1. In a workspace, load the 2 attached csv files  
2. Use "hasKind" to create kinds "SchoolsSmall50CSV" and "ParksSmall10CSV"  
3. Create a query graph for SchoolsSmall50CSV, and then join with "ParksSmall10CSV"  
4. Link "city" of Schools to "city" of Parks  
5. Click on "ParksSmall10CSV" on the query graph, the result should be

NOTE: Regardless of ordering

```text
IND01, South Street Park, , Indianapolis, IN, US
IND02, South Street Park I, , Indianapolis, IN, US
```

6. Link "state" of Schools to "state" of Parks

7. Click on "ParksSmall10CSV" on the query graph
{% endtab %}

{% tab title="Expected Results" %}
No Duplicates in the query results.

NOTE: Regardless of ordering

```text
IND01, South Street Park, , Indianapolis, IN, US
IND02, South Street Park I, , Indianapolis, IN, US
```

because there exists 1 School in city == Indianapolis, and state == IN
{% endtab %}

{% tab title="Actual Results" %}
Rows are duplicated twice: \(because there are 2 Schools in "IN" state regardless of "city"\)

NOTE: Regardless of ordering

```text
IND01, South Street Park, , Indianapolis, IN, US
IND01, South Street Park, , Indianapolis, IN, US
IND02, South Street Park I, , Indianapolis, IN, US
IND02, South Street Park I, , Indianapolis, IN, US
```
{% endtab %}
{% endtabs %}

