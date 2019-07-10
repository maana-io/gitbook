# Catalog service generates lossy and redundant storage kinds/models

{% tabs %}
{% tab title="Description" %}
The catalog service generates a storage model from the graphQL schema for a service. Fields for each kind are created for all fields of the corresponding graphQL type that take no arguments.    

This heuristic is not rich enough to infer the correct kind structures from arbitrary graphQL schemas, \(e.g. physical quantity service\), where each type may have a combination of intrinsic properties \(things that must be stored\) and functions of arbitrary arity \(including 0-ary functions\).   

This leads to both the inclusion of redundant fields in the generated kinds, and the omission of required ones.     
{% endtab %}

{% tab title="Repro Steps" %}
1. Open a new workbook.   
2. Select physical quantity service.
3. Look at the automatically generated kinds.
{% endtab %}

{% tab title="Expected Result" %}
* The SystemOfUnits kind should have a link to UnitOfMeasure, but does not.   
* The Physical Dimension kind should NOT include a self-referential link, but it does.
* The UnitOfMeasureConversion kind should NOT include a self-referential link, but it does.
* The UnitOfMeasure kind should not include isPower, hasPrefix, isSSimple, isCompatable or isUnitless fields.
* The simpleUnitOfMeasure kind should not include a isUnitless field.
{% endtab %}

{% tab title="Actual Result" %}
* The expected links between SystemOfUnits and UnitOfMeasure kinds are missing.
* Unexpected self-referential links on PhysicalDimension and UnitOfMeasureConversion exist.
* The UnitOfMeasure kind includes isPower, hasPrefix, isSSimple, isCompatable or isUnitless fields.
* The simpleUnitOfMeasure kind should includs a isUnitless field.

![Screenshot of Result](https://maanaimages.blob.core.windows.net/maana-q-documentation/image%20%281%29.png)
{% endtab %}
{% endtabs %}

