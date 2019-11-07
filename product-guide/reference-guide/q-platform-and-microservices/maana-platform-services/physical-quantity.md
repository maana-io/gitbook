# Physical Quantity

## About this service <a id="about-this-service"></a>

Maana Physical Quantity Service is used for extracting physical quantities \( a.k.a. measured quantities\) from text, and performing dimensionally safe arithmetic, unit conversions and comparisons with them. This service uses a proprietery symbolic computing engine built on top of Stanford CoreNLP's named entity recognition library \([https://nlp.stanford.edu/software/](https://nlp.stanford.edu/software/)\).

This sequence of queries extracts pressure measurements from the sample sentence, converts them into head \(in feet of sea water\) and checks to see if the result is greater than an a provided alarm threshold.:

```text
query IS_OVERPRESSURE(
  $SOURCE:String!,
  $DENSITY_OF_SEAWATER:PhysicalQuantityInput!,
  $GRAVITATIONAL_ACCELERATION:PhysicalQuantityInput!,
  $ALARM_THRESHOLD:PhysicalQuantityInput!){

  extract(source:$SOURCE){
    entity{
      name
      div(divisor:$DENSITY_OF_SEAWATER){
        div(divisor:$GRAVITATIONAL_ACCELERATION)  {
          isGTE(rhs:$ALARM_THRESHOLD,precision:3)
        }}}}}
```

Queries of this kind facilitate equational reasoning with real world measurements, and can be used to augment the engineering knowledge models. Specifically, this service facilitates equational and graph based reasoning about physical quantities, units of measure, physical dimensions and systems of units.

## Assumptions <a id="assumptions"></a>

1. Entity mentions follow standard notational conventions for products, quotients and exponentials of units of measure
2. Although aliases are allowed, no unit of measure that is not a product, power or quotient can consist of more than one token. For example: "1 Astronomical unit" would be invalid, but "1 AU" would be acceptable

## Warnings <a id="warnings"></a>

1. The service uses a constructive pattern matching algorithm to parse physical quantities from text. Acronyms, abbreviations and part numbers can easily be misidentified as units of measure. Some data cleansing may be required to get optimal performance.

## Reference Examples <a id="reference-examples"></a>

**NOTE on Fragments**: Many of the examples in this document use graphQL fragments to simplify the output specifications. Definitions of the graphQL fragments can be found in the appendix.

**NOTE on Variables**: Some examples require execution of a sequence of queries, storing intermediate results in variables to be passed to later stages. For clarity, we name the earlier stages of computation with the same name as the variable to which they are bound. For example:

```text
query FOO{ foo{ ... FooFragment }}query BAR( $FOO: FooInput ){ ... BarFragment }
```

Means, execute the query FOO, storing the result in the variable $FOO, and then call the query BAR.

### Physical Quantities <a id="physical-quantities"></a>

| Example | How do I get the normalized surface form of a physical quantity? |
| :--- | :--- |
| Info | The physical quantity service automatically normalizes the surface form of physical quantities. Use the name property of the physical quantity type to get the normalized surface form of a physical quantity. The example below demonstrates how to get the normalized surface form of a physical quantity parsed from text. |
| Query | query EXAMPLE1{parse\(source:"ten psi"\){ name }} |
| Response | { "data": { "parse": { "name": "10.0 lb/in²" }}} |

| Example | How do I get the magnitude \(numeric value\) of a physical quantity? |
| :--- | :--- |
| Info | Use the magnitude property of the physical quantity type to get the numeric value of a physical quantity. The example below demonstrates how to get the numeric value of a physical quantity parsed from text. |
| Query | query EXAMPLE2{parse\(source:"ten psi"\){ magnitude }} |
| Response | { "data": { "parse": { "magnitude": 10 }}} |

| Example | How do I get the unit of measure of a physical quantity? |
| :--- | :--- |
| Info | Use the unitOfMeasure property of the physical quantity type to get the unit of measure of a physical quantity. The example below demonstrates how to get the unit of measure of a physical quantity parsed from text. |
| Query | query EXAMPLE3{parse\(source:"ten psi"\){ unitOfMeasure{ name }}} |
| Response | { "data": { "parse": { "unitOfMeasure": { "name": "lb/in²" }}}} |

### Unit Of Measure <a id="unit-of-measure"></a>

| Example | How can I see all the available units of measure? |
| :--- | :--- |
| Info | Since the system can derive an infinite number of units of measure using multiplication, division and exponentiation, It is NOT possible to see ALL available units of measure. Instead, we can use the unitsOfMeasure query to find all the units of measure that have been explicitly defined. The physical quantity service comes out of the box with explicit definitions for the commonly used units of measure for both the MKS and Imperial systems of units. |
| Query | query EXAMPLE4{unitsOfMeasure { name }} |
| Result | { "data": { "unitsOfMeasure": \[{"name": "C"}, {"name": "m"}, { "name": "km"}, { "name": "D" }, .. AND MANY MORE \] }} |

| Example | How can I see all the available units of measure for a particular physical dimension? |
| :--- | :--- |
| Info | Since the system can derive an infinite number of units of measure using multiplication, division and exponentiation, It is NOT possible to see ALL available units of measure. |

| Example | How do I get the normalized surface form of a unit of measure? |
| :--- | :--- |
| Info | The physical quantity service automatically normalizes the surface form of units of measure. Use the name property of the UnitOfMeasure type to get the normalized surface form. The example below demonstrates how to get the normalized surface form of a unit of measure from a physical quantity parsed from text. |
| Query | query EXAMPLE5{parse\(source: "9.8 kilogram \* meter / second squared"\) { unitOfMeasure { name}}} |
| Response | { "data": { "parse": { "unitOfMeasure": { "name": "kg·m/s²"}}}} |

| Example | How do I get the aliases for a unit of measure? |
| :--- | :--- |
| Info | Use the aliases property of the UnitOfMeasure type to get the aliases for the unit of measure. Any of the returned aliases could be used interchangeably with the preferred denotation. The example below demonstrates how to get the aliases for a unit of measure from a physical quantity parsed from text. |
| Query | query EXAMPLE6{unitOfMeasure\(unitRef:{name:"mi/hr"}\) { aliases}} |
| Response | { "data": { "unitOfMeasure": { "aliases": \[ "mph"\]}}} |

| Example | How do I get the physical dimension of a unit of measure? |
| :--- | :--- |
| Info | Use the dimension property of the UnitOfMeasure type to get its physical dimension. The example below demonstrates how to get the physical dimension form of a unit of measure from a physical quantity parsed from text. |
| Query | query EXAMPLE7{unitOfMeasure\(unitRef:{name:"N"}\){dimension{name}}} |
| Response | { "data": { "unitOfMeasure": { "dimension": { "name": "FORCE"}}}} |

### Unit Of Measure Prefix <a id="unit-of-measure-prefix"></a>

| Example | How can I see all the available unit of measure prefixes? |
| :--- | :--- |
| Info | Use the unitOfMeasurePrefixes query to find all the unit of measure prefixes. The physical quantity service comes out of the box with the metric system prefixes. |
| Query | query EXAMPLE8{unitOfMeasurePrefixes{ name}} |
| Response | { "data": { "unitOfMeasurePrefixes": \[ { "name": "f"}, { "name": "p"}, { "name": "n"}, { "name": "μ"}, ... AND MANY MORE\]}} |

| Example | How do I get the preferred symbol for a unit of measure prefix? |
| :--- | :--- |
| Info | Use the name property of the UnitOfMeasurePrefix to get the preferred symbol for the prefix. The example below gets the preferred symbol for all the unit of measure prefixes in the system: |
| Query | query EXAMPLE9{unitOfMeasurePrefixes{ name}} |
| Response | { "data": { "unitOfMeasurePrefixes": \[ { "name": "f"}, { "name": "p"}, { "name": "n"}, { "name": "μ"}, ... AND MANY MORE\]}} |

| Example | How do I get the aliases for a unit of measure prefix? |
| :--- | :--- |
| Info | Use the aliases property of the UnitOfMeasurePrefix to get all the aliases for the unit of measure prefix. The example below gets the aliases for all the unit of measure prefixes in the system: |
| Query | query EXAMPLE10{unitOfMeasurePrefixes{ aliases}} |
| Response | { "data": { "unitOfMeasurePrefixes": \[ { "aliases": \[ "f", "fempto"\]}, { "aliases": \[ "p", "pico"\]}, { "aliases": \[ "n", "nano"\]}, { "aliases": \[ "μ", "u", "micro"\]}, ... AND MANY MORE\]}} |

| Example | How do I get the scaling factor for a unit of measure prefix? |
| :--- | :--- |
| Info | Use the multiplier property of the UnitOfMeasurePrefix to get all the scaling factor for the unit of measure prefix. The example below gets the multipliers for all the unit of measure prefixes in the system: |
| Query | query EXAMPLE11{unitOfMeasurePrefixes{ multiplier}} |
| Response | { "data": { "unitOfMeasurePrefixes": \[ { "multiplier": 1e-15}, { "multiplier": 1e-12}, { "multiplier": 1e-9}, { "multiplier": 0.000001}, ... AND MANY MORE\]}} |

### Physical Dimensions <a id="physical-dimensions"></a>

| Example | How can I see all the available physical dimensions? |
| :--- | :--- |
| Info | Since the system can derive an infinite number of physical dimensions using multiplication, division and exponentiation, It is NOT possible to see ALL available physical dimensions. Instead, we can use the physicalDimensions query to find all the physical dimensions that have been explicitly defined. The physical quantity service comes out of the box with over 60 of the most commonly occurring physical dimensions in engineering and scientific literature. |
| Query | query EXAMPLE12{physicalDimensions { name aliases formula}} |
| Response | { "data": { "physicalDimensions": \[ { "name": "VELOCITY", "aliases": \[\], "formula": "L¹T⁻¹"}, { "name": "ELECTRICAL\_RESISTANCE", "aliases": \[\], "formula": "L²M¹T⁻³J⁻²"}, { "name": "ABASEMENT", "aliases": \[\], "formula": "L¹T¹"}, { "name": "MOMENTUM", "aliases": \[\], "formula": "L¹M¹T⁻¹" ... AND MANY MORE},\]}} |

| Example | How do I look up a physicalDimension by its name, formula or alias? |
| :--- | :--- |
| Info | Use the physicalDimension query to search for a physical dimension based on its name, formula or alias. The example below finds a physical dimension by name: |
| Query | query EXAMPLE13{physicalDimension\(dimensionRef:{name:"ELECTRICAL\_CURRENT"}\){ formula}} |
| Response | { "data": { "physicalDimension": { "formula": "J¹"}}} |

| Example | How do I get the preferred name of a physical dimension? |
| :--- | :--- |
| Info | Use the name field of the PhysicalDimension type to get the preferred name for a physical dimension. The example below gets the preferred name of all the explicitly defined physical dimensions: |
| Query | query EXAMPLE14{ physicalDimensions{name}} |
| Response | { "data": { "physicalDimensions": \[ { "name": "VELOCITY"}, { "name": "ELECTRICAL\_RESISTANCE"}, { "name": "ABASEMENT"}, { "name": "MOMENTUM"}, ... AND MANY MORE\]}} |

| Example | How can I get the aliases for a physical dimension? |
| :--- | :--- |
| Info | Use the name field of the PhysicalDimension type to get the preferred name for a physical dimension. The example below gets the aliases of all the explicitly defined physical dimensions having the formula "L²M¹T⁻²": |
| Query | query EXAMPLE15{physicalDimension\(dimensionRef:{formula:"L²M¹T⁻²"}\){ aliases}} |
| Response | { "data": { "physicalDimension": { "aliases": \[ "ENERGY" "WORK", "TORQUE"\],}}} |

| Example | How can I get the formula for a physical dimension? |
| :--- | :--- |
| Info | Use the name formula of the PhysicalDimension type to get the formula for a physical dimension. The example below gets the formula of the explicitly defined physical dimension of "MOLAR\_HEAT\_CAPACITY": |
| Query | query EXAMPLE16{physicalDimension\(dimensionRef:{name:"MOLAR\_HEAT\_CAPACITY"}\){ formula}} |
| Response | { "data": { "physicalDimension": { "formula": "L²M¹T⁻²ϴ⁻¹N⁻¹"}}} |

### Systems Of Units <a id="systems-of-units"></a>

| Example | How can I get a list of all the systems of units? |
| :--- | :--- |
| Info | Use the systemsOfUnits query to get a list of all the systems of units. For example the query below gets a list of all the names and descriptions of all the systems of units. |
| Query | query EXAMPLE17{systemsOfUnits{ name, description}} |
| Response | {"data": { "systemsOfUnits":\[{"name": "mks","description": "mks \(meter-kilogram-second\) system" },{"name": "Imperial","description": "Imperial \(American\) Unit System"},{"name": "oil and gas","description": "Oil and Gas domain specific units of measure"}\]}} |

| Example | How can I see all the units of measure in a system of units? |
| :--- | :--- |
| Info | Since the system can derive an infinite number of units of measure using multiplication, division and exponentiation, It is NOT possible to see ALL the units of measure in a system of units. Instead, you can use the units field of the SystemOfUnits type to get the list of explicitly defined units of measure that occur in that system of units. |
| Query | query EXAMPLE18{systemOfUnits\(systemRef:{name:"Imperial"}\){ units{ name}}} |
| Response | { "data": { "systemOfUnits": { "units": \[ { "name": "ft"}, { "name": "in"}, { "name": "mi"}, { "name": "yd"}\]}}} |

| Example | How can I see all the unit of measure prefixes in a system of units? |
| :--- | :--- |
| Info | Use the prefixes field of the SystemOfUnits type to get the list of unit of measure prefixes in that system of units. The example below demonstrates how to find all the unit of measure prefixes in the mks unit system: |
| Query | query EXAMPLE19{systemOfUnits\(systemRef:{name:"mks"}\){ prefixes{ name}}} |
| Response | { "data": { "systemOfUnits": { "prefixes": \[ { "name": "f"}, { "name": "p"}, { "name": "n"}, { "name": "μ"}, ... AND MANY MORE\]}}} |

### Parsing <a id="parsing"></a>

| Example | How do I convert that string to a physical quantity? |
| :--- | :--- |
| Info | Use the parse query to convert a string into a physical quantity. The parse query can be used when you have a single string that is a surface form of an entity mention -- the parse query will throw an error if the provided string is not a surface form for some physical quantity. |
| Query | EXAMPLE20{parse\(source:"400 psi"\){ name}} |
| Response | { "data": { "parse": { "name": "400.0 lb/in²"}}} |

| Example | How do I convert the string to a physical quantity only if its unit of measure is in a particular system of units? |
| :--- | :--- |
| Info | Use the optional systemRefs parameter to specify either the id or name of the required systems of units. If no systemRefs parameter is provided, the parser uses all available systemsOfUnits. |
| Query | query IMPERIAL{systemOfUnits\(systemRef:{name:"Imperial"}\){ ... SystemOfUnitsFragment}} query EXAMPLE21\($IMPERIAL:SystemOfUnitsInput\){ parse\(source:"400 psi",systemInputs:\[$IMPERIAL\]\){ name}} |
| Response | { "data": { "parse": { "name": "400.0 lb/in²"}}} |

| Example | How do I convert the string to a physical quantity only if it has a specific physical dimension? |
| :--- | :--- |
| Info | Use the optional dimensionInput parameter to specify either the name or formula of the required physical dimension. If no dimensionRef parameter is provided, the parser admits all physical dimensions. |
| Query | query LENGTH{physicalDimension\(dimensionRef:{name:"LENGTH"}\){ ... PhysicalDimensionFragment }} query EXAMPLE22\($LENGTH:PhysicalDimensionInput\){ parse\(source:"400 meters",dimensionInputs:\[$LENGTH\]\){ name }} |
| Response | { "data": { "parse": { "name": "400.0 lb/in²"}}} |

### Extraction <a id="extraction"></a>

| Example | You have a list of strings, each which may contain zero or many physical quantities. How do you extract all the physical quantities from the source text? |
| :--- | :--- |
| Info | Use the extract query to get all the entity mentions from the text. The extract method can be used to find entity mentions in a list of string literals, or the field of a kind. The extractor will find all the physical quantity mentions in each string \(or instance of a field\) and return a list of the results. |
| Query | query EXAMPLE23{extractBatch\(sources: \[ "the airspeed of the plane was 350 mph as it passed through 3000 meters.", "The minimum runway length is 7500 feet."\]\) { entity { name}} } |
| Result | { "data": { "extractBatch": \[ \[{ "entity": { "name": "350.0 mi/hr"}}, { "entity": { "name": "3000 m"}}\], \[{ "entity": { "name": "7500.0 ft"}}\]\]}} |

| Example | You have a list of strings, each which may contain zero or more entity mentions. How do extract all the physical quantities from the source text only if their unit of measure is in the Imperial unit system? |
| :--- | :--- |
| Info | Use the optional systemInputs parameter to specify either the id or name of the required systems of units. If no systemInputs parameter is provided, the extractor uses all available systemsOfUnits. |
| Query | query IMPERIAL{systemOfUnits\(systemRef:{name:"Imperial"}\){ ... SystemOfUnitsFragment}} query EXAMPLE24\($IMPERIAL:SystemOfUnitsInput\){ extractBatch\(sources: \["the airspeed of the plane was 350 mph as it passed through 3000 meters.","The minimum runway length is 7500 feet."\], systemInputs:\[$IMPERIAL\]\) { entity { name}}} |
| Response | { "data": { "extractBatch": \[ { "entity": { "name": "350.0 mi/hr"}}, { "entity": { "name": "7500.0 ft"}}\]}} |

| Example | You have a list of strings, each which may contain zero or more entity mentions. How do extract all the physical quantities from the source text only if they have dimensions of length? |
| :--- | :--- |
| Info | Use the optional dimensionInputs parameter to specify either the name or formula of the required physical dimension. If no dimensionInputs parameter is provided, the extractor admits all physical dimensions. |
| Query | query EXAMPLE25{extractBatch\(sources: \[ "the airspeed of the plane was 350 mph as it passed through 3000 meters.", "The minimum runway length is 7500 feet."\], dimensionInputs:\[{name:"LENGTH",formula:"L¹"}\]\) { entity { name}}} |
| Response | { "data": { "extractBatch": \[ { "entity": { "name": "3000.0 m"}}, { "entity": { "name": "7500.0 ft"}}\]}} |

| Example | You have a list of strings, each which may contain zero or more entity mentions. After extracting the entity mentions, how do you know where they occur in the source text? |
| :--- | :--- |
| Info | The fromKind, fromField, fromInstance, and fromString fields of the EntityMention type provide locators to the source text. The fromOffset field of the entity EntityMention type provides the distance from the start of the string \(in characters\) to the start of the entity mention. The fromSpan field of the EntityMention type provides the length of the entity mention \(in characters\). |
| Query | query LENGTH{physicalDimension\(dimensionRef:{name:"PRESSURE"}\){ ... PhysicalDimensionFragment }} query EXAMPLE26\($LENGTH:PhysicalDimensionInput\){ extractBatch\(sources: \[ "the airspeed of the plane was 350 mph as it passed through 3000 meters.", "The minimum runway length is 7500 feet."\], dimensionInputs:\[$LENGTH\] \) { entity { name} fromSpan, fromOffset}} |
| Response | { "data": { "extractBatch": \[ \[ { "entity": { "name": "3000.0 m"}, "fromSpan": "12", "fromOffset": "59"}\], \[{ "entity": { "name": "7500.0 ft"}, "fromSpan": "10", "fromOffset": "29"}\]}} |

### Conversions <a id="conversions"></a>

| Example | How do I convert a physical quantity to a different unit of measure? |
| :--- | :--- |
| Info | You can use the "convertTo" query, "convertTo" field, or "convertTo" argument to convert a physical quantity to a specific unit of measure. The examples below show examples of how to use each method to convert a pressure from atmospheres to gauge pressure. |
| using nested calls | query PSI{ unitOfMeasure\(unitRef:{name:"lb/in²"}\){ ...UnitOfMeasureFragment }} query EXAMPLE27\($PSI:UnitOfMeasureInput!\){parse\(source:"100 mbar"\){ convertTo\(toUnitInput:$PSI\){ roundTo\(precision:2\){name}}}} |
| using arguments | query PSI{ unitOfMeasure\(unitRef:{name:"lb/in²"}\){ ...UnitOfMeasureFragment }} query EXAMPLE28\($PSI:UnitOfMeasureInput!\){convertTo\(input:{parseFrom:"100 mbar"},toUnitInput:$PSI,precision:2\){ name}} |
| Response | { "data": { "convertTo": { "name": "1.5 lb/in²" }}} |

| Example | How can I tell if a physical quantity can be converted to a specific unit of measure? |
| :--- | :--- |
| Info | Use the canBeConverted to field of the UnitOfMeasure type to test if two units are interconvertible. The following query demonstrates how to test if a physical quantity can be converted to units of "psi' |
| Query | query PSI{ unitOfMeasure\(unitRef:{name:"lb/in²"}\){ ...UnitOfMeasureFragment }} query EXAMPLE29\($PSI:UnitOfMeasureInput!\){canBeConvertedTo\(input:{parseFrom:"100 mbar"}, toUnitInput:$PSI\)} |
| Response | { "data": { "canBeConvertedTo": true } } |

### Arithmetic <a id="arithmetic"></a>

| Example | Add physical quantities with different dimensions |
| :--- | :--- |
| Info | The physical quantity service will perform the necessary unit conversions for you, so long as the units are dimensionally consistent |
| Query | query EXAMPLE30{sum\(summands: \[{parseFrom: "12 inch"}, {parseFrom: "1 foot"}, {parseFrom: "1/3 yard"}\], precision: 2\) { name}} |
| Response | { "data": { "sum": { "name": "36.0 in"}}} |

| Example | Multiplication and division |
| :--- | :--- |
| Info | When you pass arguments that have different units or physical dimensions, computer algebra on units of measure and physical dimensions automatically constructs the correct unit of measure for the returned physical quantity |
| Query | query EXAMPLE31{product\(factors: \[{parseFrom: "12 inch"}, {parseFrom: "1 Hz"}, {parseFrom: "1/3 acre"}\], precision: 2\) { name, unitOfMeasure { dimension { formula}}}} |
| Response | { "data": { "product": { "name": "4.0 Hz·acre·in", "unitOfMeasure": { "dimension": { "formula": "L³T⁻¹"}}}}} |

### Size Comparisons <a id="size-comparisons"></a>

| Example | Comparing size without converting units |
| :--- | :--- |
| Info | The physical quantity service will perform the necessary unit conversions for you, as long as the units are dimensionally consistent |
| Query | query REFERENCE{ parse\(source:"35 cm"\) { ... PhysicalQuantityFragment }} query EXAMPLE32\($REFERENCE:PhysicalQuantityInput!\){extractBatch\(sources: \["1 inch","1 foot","1 yard"\]\) { entity{ isGT\(rhs:$REFERENCE\)}}} |
| Response | { "data": { "extractBatch": \[ \[ { "entity": { "isGT": false } } \], \[ { "entity": { "isGT": false } }\], \[{ "entity": { "isGT": true } } \] \] } } |

## More Information <a id="more-information"></a>

Visit the Maana Cookbook for a [hands-on tutorial on how to use the Physical Quantity Service​](https://maana.gitbook.io/q/maana-q-cookbook/advanced-recipes/extracting-physical-quantities)

## Appendix <a id="appendix"></a>

### GraphQL Fragments <a id="graphql-fragments"></a>

```text
fragment PhysicalDimensionFragment on PhysicalDimension {
  name
  aliases
  formula
}

fragment UnitOfMeasurePrefixFragment on UnitOfMeasurePrefix {
  name
  aliases
  multiplier
}

fragment UnitOfMeasureFragment on UnitOfMeasure {
  name
  aliases
  factors {
    base {
      name
      aliases
      dimension { ... PhysicalDimensionFragment }
      siUnitConversion { multiplier offset }
    }
    prefix { ... UnitOfMeasurePrefixFragment }
    exponent
}}

fragment PhysicalQuantityFragment on PhysicalQuantity{
  magnitude
  unitOfMeasure{ ... UnitOfMeasureFragment }
}

fragment SystemOfUnitsFragment on SystemOfUnits{
  name
  description
  units{ ... UnitOfMeasureFragment }
  prefixes{ ... UnitOfMeasurePrefixFragment }   
}
```

​[  
](https://maana.gitbook.io/q/~/drafts/-L_Q5gV0LFJTEe_bmaXC/primary/product-guide/reference-guide/q-platform-and-microservices/maana-platform-services/fact-recognition-and-fr-bot)

