# RC1-008: ConvertGQLtoKinds fails on types with union fields

{% tabs %}
{% tab title="Description" %}
There is no path in convertGQLtoKinds for processing Unions.  Fields that are union type get labeled as type Kind while no Kind gets produced for them. 
{% endtab %}

{% tab title="Repro Steps" %}
1. Stand up a graphQL service with a Union in its schema.
2. Add that service to Maana Q.
{% endtab %}

{% tab title="Expected Result" %}
The Kinds and Functions are created for the Service schema; the service is added to the system.

```text
function getTypeInformation(type, kinds) {
  const isNoNull = type instanceof GraphQLNonNull
  const isList = (isNoNull ? type.ofType : type) instanceof GraphQLList
  const namedType = getNamedType(type)
  const isScalar = namedType instanceof GraphQLScalarType
  const isEnum = namedType instanceof GraphQLEnumType
  const typeName = namedType.toString()

  let modifiers = []
  if (isNoNull) modifiers.push(FieldModifiers.NONULL)
  if (isList) modifiers.push(FieldModifiers.LIST)

  let systemType = FieldTypes.KIND
  if (isScalar) {
    systemType = typeName.toUpperCase()
  } else if (isEnum) {
    systemType = FieldTypes.STRING
  }
```
{% endtab %}

{% tab title="Actual Result" %}
Catalog Service fails to convert the schema to Kinds and Functions when convertGQLtoKinds process a field with a Union type.
{% endtab %}

{% tab title="Resolved" %}
Issue has been resolved.  

{% hint style="info" %}
If you experience this issue while working in Maana Q, please file a [bug report](https://maana-ue.gitbook.io/product/reference-docs/report-bugs).
{% endhint %}
{% endtab %}
{% endtabs %}

