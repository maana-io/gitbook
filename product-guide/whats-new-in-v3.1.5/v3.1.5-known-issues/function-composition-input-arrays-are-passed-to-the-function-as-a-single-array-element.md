# RC1-011: Function composition input arrays are passed to the function as a single array element

{% tabs %}
{% tab title="Description" %}
Function composition input is not treated as array when it should.
{% endtab %}

{% tab title="Repro Steps" %}
1. Using the Maana Natural Language Processing service, drag the function "extractBatch" onto the knowledge graph.  

2. In the "sources" field add the text \["John lives in Seattle", "Sergey lives in New York"\] or variation "John lives in Seattle", "Sergey lives in New York". 

3.Run the function.  The function is treated as a single string.  The output produced is:

![](https://jira.corp.maana.io/secure/attachment/23491/23491_Screen+Shot+2019-01-24+at+1.33.43+PM.png)

4. Where there should actually be 2 elements to the array \[\[\],\[\]\] instead there is 1 \[\] \(indicating the input was treated as a single string\).  The graphql result from the same query:

```text
query {
  extractBatch(sources : ["John lives in Seattle", "Sergey lives in New York"]){     entityName     surfaceForm   }
}
is
{
"data": {
"extractBatch": [
  [
   {     "entityName": "Person",     "surfaceForm": "John"     }
,
   {     "entityName": "Location",     "surfaceForm": "Seattle"     }
  ],
  [
   {     "entityName": "Person",     "surfaceForm": "Sergey"     }
,
   {     "entityName": "Location",     "surfaceForm": "New York"     }
  ]
]
}
}
```

The important point is that the function should return 2 elements to the array, but instead only returns 1.  There should be 1 for each sentence.
{% endtab %}

{% tab title="Expected Result" %}
There should be one array element for each input in the result \(for 2 total elements\).
{% endtab %}

{% tab title="Actual Result" %}
There is 1 array element total indicating that the input was treated as a single string.
{% endtab %}
{% endtabs %}

