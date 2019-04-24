# RC2-008: Error adding instances if a Kind field cardinality modifier was perviously changed

{% tabs %}
{% tab title="Description" %}
Error when adding instances if a Kind field cardinality modifier was perviously changed from either LIST to non-LIST or non-LIST to LIST

Remediation:

Create new field with needed type \(i've created 'equipment2: \[Equipment!\]!'\), delete old field.

**`*NOTE*`**`Until the old (broken) field is deleted, user will not be able to write to this kind.`
{% endtab %}

{% tab title="Repro Steps" %}
Add instances to a Kind via Data Load or CRUD mutation
{% endtab %}

{% tab title="Expected Results" %}
Instances added to the Kind
{% endtab %}

{% tab title="Actual Results" %}
{  
"data":{ "updateRig": null }

,  
"errors": \[  
{ "message": "Error PUTting instances using schema: \[\{\"rowKey\":\"30002\",\"id\":\"xyzUUID\",\"kindId\":\"xyzUUID\",\"instanceTableId\":30001,\"ordinal\":0,\"name\":\"id\",\"description\":\"id\",\"type\":\"ID\",\"typeKindId\":\"\",\"modifiers\":\[\"NONULL\"\],\"displayAs\":\[\],\"hide\":false,\"autoFocus\":false,\"readonly\":true,\"isDeleted\":false}

...
{% endtab %}
{% endtabs %}

