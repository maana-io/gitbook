---
description: Computational Knowledge Graph
---

# Introduction to Kinds and Functions

---------------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [x] Power Point Slides \(**not needed**\)
* [x] Workspaces \( [https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases](https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases)\) 
* [x] Step-by-Step Instructions for Learning Assistant \(Complete\)
* [x] Case description \(**complete**\)
* [ ] Revisit content below \(**pending**\)
* [ ] Possibly add here use case shared by Logan at Show and Tell \(google maps visualization of crime vs. real estate in Sacramento - deciding where to buy property looking at the map\). Need to check if assistant service that is needed can be deployed to cstraining01 \(**pending**\)

---------------------------------------------------------------------------------------------------------------



**Use Case Description:**  

The aim of this lesson is to introduce Kinds and Functions by creating a means by which to calculate the distance between to Geo Coordinates.  Additionally we will extend the example to accommodate names of places.  In order to carry out the computations we will leverage a service already part of our Maana Q deployment.   

**Step by Step Instructions**

Pre requisites 

1. Workspace created 
2. Services, distance-lambda-demo added to inventory 
3. GeoCoordinate Kind and Distance Kind created 

**Step 1:** Create Kinds  

1. Above the canvas click on the create kind button, a blue box will appear 
2. Create a GeoCoordinate kind with properties; 
   * lat  FLOAT 
   * long FLOAT 
3. Repeat to create a Distance kind with properties; 
   * value FLOAT 
   * distanceUnit STRING 

**Step 2:** Create “top level” function 

1. Above the canvas click on the create function button, a green function box will appear.  
2. Give the function a name e.g “distanceBetweenCoordinates”.  
3. Add an inputs by clicking on the line below the “field” heading  
   * origin GEOCOORDINATE 
   * target GEOCOORDINATE 
   * Specify the as type Distance 
4. Click Save

**Step 3:** Create Function Calculation for distanceBetweenCoordinates  

1. Click on the 4 arrows located in the top right hand corner of the function box. This will take us to a canvas where we can begin to “wire up” our function 
2. From the inventory locate the distanceBetweeenCoordinates Function from the lambda-distance-demo service 
3. Drag the function onto the canvas 
4. Connect the inputs and output 

**Step 4:** Test the distanceBetweenCoordinates Function 

1. Click on Top Level PQ and select the distanceBetweenGeoCoordinates Function 
2. In the right hand panel add an origin and target \(be sure to add the ID field\) 
3. Click Run 
4. Observe the results in the function results panel at the bottom of the screen  

**Step 5:** Add distanceBetweenAddresses Function 

1. Click on Top Level PQ and add the function, distanceBetweenAddresses 
2. Inputs:  
   * origin STRING 
   * target STRING 
3. Output: 
   * Distance 

**Step 6:** Add getGeoCoordinatesByName function to distanceBetweenAddresses Function 

1. Open the distanceBetweenAddresses function and add a new function, getGeoCoordinatesByName 
2. Inputs: 
   * name STRING  
3. Output: 
   * GEOCOORDINATE 
4. Open this function and add getGeoCoordinatesByName function from the lambda-distance-demo service 
5. Wire the inputs and output 

**Step 7:** Add a second getGeoCoordinatesByName function and finish 

1. From the inventory expand the functions list 
2. Drag getGeoCoordinatesByName onto the canvas 
3. Wire the inputs of both instances 
4. Add the distanceBetweeenCoordinates Function from the lambda-distance-demo service 
5. Wire the inputs and output 

**Step 8:** Test the distanceBetweenAddresses 

1. Click on Top Level PQ and highlight the function 
2. In the right hand panel enter values for origin and target 
   * Origin = “London” 
   * Target = “Birmingham” 
3. Click run 
4. Observe the results in the function results panel. 



Link to Step by Step Recordings:

[https://maanainc.app.box.com/folder/92358696747](https://maanainc.app.box.com/folder/92358696747)







----------------------

Using Kinds and Function to build a knowledge graph

Major concepts:

**Kind** - represent a specific interpretation of a concept which have a collection of fields used to describe their attributes. Ex: a kind called ‘City’ may consist of name, latitude, longitude 

Input and Outputs

**Input Fields**

The input fields of a Function represent the input that is expected to a Function. The Field column has the name of the field and the Type column has the type \(including modifiers\) that is expected as input to that field.

There are also two modifiers indicated in the Type column: required and list. If the Type has an exclamation mark \(**!**\), the field is required to have a value. If the Type is surrounded in square brackets \(**\[\]**\), the field value is a list. Note that both can be present. Thus **\[STRING!\]!** means the field requires a list of Strings to be provided, where each value in the list cannot be null and the list itself must not be null.

**Output Field**

The output field represents the expected output from a Function. Only the type is editable on the output field and there is only one output. The output field type has the same modifiers as the input fields. In the screenshot above, the output is a String.

Function

\*\*\*\*[**Authored functions** ](https://app.gitbook.com/@maana/s/q/~/edit/drafts/-Lss1wojMQWwITyvTgMq/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/understanding-functions#understanding-maana-functions)

\*\*\*\*[**Imported functions**](https://app.gitbook.com/@maana/s/q/~/edit/drafts/-Lss1wojMQWwITyvTgMq/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/understanding-functions#understanding-maana-functions)\*\*\*\*

**Computational knowledge graph** - separates the structure and computations to be performed from the data itself; It enables a fluidity of modeling, allowing data from any source or format to be seamlessly integrated, searched, analyzed, operationalized and re-purposed; Each resulting model is a combination of subject-matter expertise, relevant data, and the algorithms to be performed; It’s dynamic because it can represent conceptual and computational models; It’s designed to perform complex transformations and calculations at interactive speeds, making it a game-changing technology for agile development knowledge applications

**Creating Kinds to Build a Knowledge Graph** 

There are two ways to create the kinds of data used as the building blocks for your Knowledge Graph:

1. [The Data-First Approach](https://app.gitbook.com/@maana/s/q/~/edit/drafts/-Lss1wojMQWwITyvTgMq/v/3.2.1/product-guide/reference-guide/technical-design-and-architecture/kinds-and-fields/kind-approaches#data-first-approach)
2. [The Model-First Approach](https://app.gitbook.com/@maana/s/q/~/edit/drafts/-Lss1wojMQWwITyvTgMq/v/3.2.1/product-guide/reference-guide/technical-design-and-architecture/kinds-and-fields/kind-approaches#data-first-approach) 

-----------------------------------

\*\*\*\*

