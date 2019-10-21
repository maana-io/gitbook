---
description: Computational Knowledge Graph
---

# CKG

Major concepts:

**Kind** - represents a specific interpretation of a concept which have a collection of fields used to describe their attributes. Ex: a kind called ‘City’ may consist of name, latitude, longitude 

\*\*\*\*

**Function**

[Authored functions ](https://maana.gitbook.io/q/product-guide/getting-started-with-maana/building-knowledge-layers/understanding-functions#authored-functions)

[Imported functions](https://maana.gitbook.io/q/product-guide/getting-started-with-maana/building-knowledge-layers/understanding-functions#imported-functions)

\*\*\*\*

**Function Input and Outputs**

**Input Fields**

The input fields of a Function represent the input that is expected to a Function. The Field column has the name of the field and the Type column has the type \(including modifiers\) that is expected as input to that field.

There are also two modifiers indicated in the Type column: required and list. If the Type has an exclamation mark \(**!**\), the field is required to have a value. If the Type is surrounded in square brackets \(**\[\]**\), the field value is a list. Note that both can be present. Thus **\[STRING!\]!** means the field requires a list of Strings to be provided, where each value in the list cannot be null and the list itself must not be null.

**Output Field**

The output field represents the expected output from a Function. Only the type is editable on the output field and there is only one output. The output field type has the same modifiers as the input fields. In the screenshot above, the output is a String.



**CKG \(**computational knowledge graph\) - separates the structure and computations to be performed from the data itself; It enables a fluidity of modeling, allowing data from any source or format to be seamlessly integrated, searched, analyzed, operationalized and re-purposed; Each resulting model is a combination of subject-matter expertise, relevant data, and the algorithms to be performed; It’s dynamic because it can represent conceptual and computational models; It’s designed to perform complex transformations and calculations at interactive speeds, making it a game-changing technology for agile development knowledge applications

**Creating Kinds to Build a Knowledge Graph** 

There are two ways to create the kinds of data used as the building blocks for your Knowledge Graph:

1. The Data-First Approach
2. The Model-First Approach

