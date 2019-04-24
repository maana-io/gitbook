# RC1-028: Q loader - does not process a XLSX file

{% tabs %}
{% tab title="Description" %}
XLSX \(_\*_X\) files are compressed and it's impossible to determine exactly their decompression ratio and therefore if they will exceed the MAX\_OUTPUT\_SIZE. 
{% endtab %}

{% tab title="Repro Steps" %}
* Drag and drop a large xlsx file to the Knowledge Graph.
{% endtab %}

{% tab title="Expected Result" %}
* File ingestion throws an error if size exceeds MAX\_OUTPUT\_SIZE allowed.
{% endtab %}

{% tab title="Actual Result" %}
* The file does not process to create an instance of Kind Document if once decompressed, the file exceeds MAX\_OUTPUT\_SIZE.
{% endtab %}
{% endtabs %}

