# Services

Maana Q includes a Catalog of services that are useful generically or within specialized domains, such as oil & gas, manufacturing, transportation, etc.  Software development is able to go more quickly when there are ready-made components that can be taken as-is or easily modified for other projects.

Several important and common services are included in every Maana Q instance and described below.

## Standard Services

### Maana Common

The Maana Common service provides foundational models for everyday concepts, such as Person, Location, Organization, Currency, etc.

### Maana Scalars

The Maana Q Scalar service provide basic operations for the core data types:

* Boolean
* Integer
* Float
* String
* Identity
* Date / Time
* JSON

For each of these, convenience functions are provided for:

* Required/optional coercion
* Serialization/deserialization
* List operations
* Constants \(True/False, 0-10, etc.\)
* Type-specific operations
  * Boolean: AND, OR, XOR, NOT
  * String: concat, reverse, contains
  * ...

