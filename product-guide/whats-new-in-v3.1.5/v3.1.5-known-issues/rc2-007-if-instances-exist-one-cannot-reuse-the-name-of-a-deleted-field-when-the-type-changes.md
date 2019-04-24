# RC2-007: If instances exist, one cannot reuse the name of a deleted field when the type changes

{% tabs %}
{% tab title="Description" %}
If instances exist, one cannot reuse the name of a deleted field when the type changes
{% endtab %}

{% tab title="Repro Steps" %}


1. Create a new kind
2. Add a field of type STRING
3. Add a field of type INT
4. Save Kind
5. Add instance data to Kind \(STRING and INT\)
6. Edit kind, delete field you created of type INT
7. Save Kind
8. Edit kind, add a field with the same name as deleted field - make the type DATE
9. Save Kind
10. Try and add data \(STRING and DATE\)
{% endtab %}

{% tab title="Expected Results" %}
Instance data is added.
{% endtab %}

{% tab title="Actual Results" %}
error

```text
[io.maana.ckg.server.xyzUID] 
Error handling request: {"message":"Variable \"$addInstanceInput\" 
got invalid value {\"kindId\":\"xyzUUID\"
,\"fieldIds\":[\"xyzUUID\"
,\"xyzUID\",\"xyzUUID\"
,\"xyzUID\",\"xyzUUID\"]
,\"fieldValues\":[{\"ID\":\"AAAAA1-2\"},{\"STRING\":\"String A1\"}
,{\"INT\":\"2019-02-02\"},{\"DATE\":\"2019-02-02\"}
,{\"DATE\":\"2019-02-02\"}],\"id\":\"AAAAA1-2\"}; 
Expected type Int at value.fieldValues[2].INT; 
Int cannot represent non 32-bit signed integer value: 2019-02-02"
,"locations":[{"line":2,"column":3}],"path":["addAAAAA"]
,"stack":["Error: Variable \"$addInstanceInput\" 
got invalid value {\"kindId\":\"xyzUUID\"
,\"fieldIds\":[\"xyzUUID\",\"xyzUUID\",\"xyzUUID\",\"xyzUUID\"
,\"xyzUUID\"],\"fieldValues\":[{\"ID\":\"AAAAA1-2\"}
,{\"STRING\":\"String A1\"},{\"INT\":\"2019-02-02\"},
```
{% endtab %}
{% endtabs %}

