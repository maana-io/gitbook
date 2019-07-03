# RC1-029: Previously created workspace not recognized as a service when searched for

{% tabs %}
{% tab title="Description" %}
When Searching for a workspace using ID it only shows the workspace and not the service hence i can not drag it into my inventory in another workspace. See pictures below.

When searching for a workspace by name it doesn't show anything at all.

![Workspaces Screen](https://maanaimages.blob.core.windows.net/maana-q-documentation/workspace%20screen.png)



![Services Screen](https://maanaimages.blob.core.windows.net/maana-q-documentation/services%20screen.png)
{% endtab %}

{% tab title="Repro Steps" %}
1. Go to any new work space.
2. Search for 06a49254-915a-4335-80c2-d2d5383f745f Note how search finds a workspace but not a service.
3. If you try searching for MD\_PDM\_01 instead you get nothing.
{% endtab %}

{% tab title="Expected Result" %}
Search should also show a Service named MD\_PDM\_01 which can then be dragged into inventory.
{% endtab %}

{% tab title="Actual Result" %}
Search only shows the workspace and not the service, hence you cannot drag it into  inventory in another workspace.
{% endtab %}

{% tab title="Resolved" %}
Issue has been resolved.  

{% hint style="info" %}
If you experience this issue while working in Maana Q, please file a [bug report](https://maana-ue.gitbook.io/product/reference-docs/report-bugs).
{% endhint %}
{% endtab %}
{% endtabs %}

