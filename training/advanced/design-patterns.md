# Design Patterns

presenter: Roie

**Case Description:**

In this example, we use MaanaQ to introduce concepts and different design patterns for creating the domain models. 

1. Identity
   1. Every Kind must have an identity property and every Individual \(instance\) must have a unique identity value
   2. Often, there is a natural identity.  What are the identities of the following Kinds:
      1. ZipCode
      2. PhoneNumber
      3. URL
      4. EmailAddress
      5. AudioEncoding 
2. Specialization and Enrichment
   1. Start with a basic concept \(Kind\) and create additional Kinds that refine it, e.g., Part, RotatingPart, HydraulicPart, ElectricalPart, RotatingElectricalPart, ...
   2. The base concept, e.g., Part, contains all the common properties/relations for parts in general
   3. The specialized \(or enriched\) concepts, e.g., RotatingPart, encompasses the base concept \(Part\), but extends it in some way, e.g., maxRotationalVelocity, which doesn't apply to all part in general, only a **subset** of them
3. Unions
   1. Along with specialization, we often need to have a collection of a concept or any of its specializations
      1. e.g., if we simply had a collection of Parts, we would not be able to distinguish RotatingPart from ElectricalPart
   2. The solution is to create a new type called a union which contains relations for each of the allowed specializations, for which there will only ever be one
      1. e.g., PartUnion { electricalPart: ElectricalPart, rotatingPart: RotatingPart, hydraulicPart: HydraulicPart, rotatingElectricalPart: RotatingElectricalPart }
   3. A union can now be used as a relation or in a function as any other Kind
      1. e.g., WorkOrder { part: PartUnion, ... }
4. Concept Translation \(or Concept Mapping\)
   1. Identifying corresponding concepts from other ontologies
   2. Reshaping concepts - picking properties from one or more Kinds to construct a new Kind
5. Operating on Lists \(parallelization\) 
   1. Mapping - Iterate over a list of items to enrich a set of elements \(this is similar to creating a function in excel and applying it to a column\)  
   2. Filtering - Apply logical conditions to reduce a set of of elements 



