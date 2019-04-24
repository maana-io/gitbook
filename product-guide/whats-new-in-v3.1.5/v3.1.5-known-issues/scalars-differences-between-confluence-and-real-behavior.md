# RC1-005: Scalars - Differences between confluence & real behavior

{% tabs %}
{% tab title="Description" %}
Please confirm that it is expected.
{% endtab %}

{% tab title="Repro Steps" %}
Upload date values via CLI:  
id,test  
1,2007-10-29  
2,2007.10.29  
3,2007/10/29  
4,10-29-07  
5,20071029
{% endtab %}

{% tab title="Expected Result" %}
Only first one is good \(only this format described as valid ion confluence\).
{% endtab %}

{% tab title="Actual Result" %}
All values are uploaded, checked from the UI. PFA.
{% endtab %}

{% tab title="Resolved" %}
Issue has been resolved.  

{% hint style="info" %}
If you experience this issue while working in Maana Q, please file a [bug report](https://maana-ue.gitbook.io/product/reference-docs/report-bugs).
{% endhint %}
{% endtab %}
{% endtabs %}

