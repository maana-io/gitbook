# RC1-013: Large Document Ingesting

{% hint style="info" %}
Disable indexing during any large document ingestion, or there will be perf issues and possibly ingestion failures. The solution is either manually reindex or re-enable indexing on the Kind. Manual reindexing is the preferred solution.
{% endhint %}

