---
description: Computational Knowledge Graph
---

# Introduction to Kinds and Functions

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

   [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step1_addKinds.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20Step%201%20-%20Add%20Kinds.gif)



**Step 2:** Create “top level” function 

1. Above the canvas click on the create function button, a green function box will appear.  
2. Give the function a name e.g “distanceBetweenCoordinates”.  
3. Add an inputs by clicking on the line below the “field” heading  
   * origin GEOCOORDINATE 
   * target GEOCOORDINATE 
   * Specify the as type Distance 
4. Click Save

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step2_topLevelFunction.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%202%20top%20level%20func.gif)

**Step 3:** Create Function Calculation for distanceBetweenCoordinates  

1. Click on the 4 arrows located in the top right hand corner of the function box. This will take us to a canvas where we can begin to “wire up” our function 
2. From the inventory locate the distanceBetweeenCoordinates Function from the lambda-distance-demo service 
3. Drag the function onto the canvas 
4. Connect the inputs and output 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step3_wireUpFunction.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%203%20-%20wire%20up%20func.gif)

**Step 4:** Test the distanceBetweenCoordinates Function 

1. Click on Top Level PQ and select the distanceBetweenGeoCoordinates Function 
2. In the right hand panel add an origin and target \(be sure to add the ID field\) 
3. Click Run 
4. Observe the results in the function results panel at the bottom of the screen  

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step4_testDistanceCalculation.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%204%20test%20distance%20calc.gif)

**Step 5:** Add distanceBetweenAddresses Function 

1. Click on Top Level PQ and add the function, distanceBetweenAddresses 
2. Inputs:  
   * origin STRING 
   * target STRING 
3. Output: 
   * Distance  

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step5_distanceByAddressFunction.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%205%20distance%20by%20addess%20func.gif)

**Step 6:** Add getGeoCoordinatesByName function to distanceBetweenAddresses Function 

1. Open the distanceBetweenAddresses function and add a new function, getGeoCoordinatesByName 
2. Inputs: 
   * name STRING  
3. Output: 
   * GEOCOORDINATE 
4. Open this function and add getGeoCoordinatesByName function from the lambda-distance-demo service 
5. Wire the inputs and output 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step6_createFirstStepFunction.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%206%20create%20first%20step%20func.gif)

**Step 7:** Add a second getGeoCoordinatesByName function and finish 

1. From the inventory expand the functions list 
2. Drag getGeoCoordinatesByName onto the canvas 
3. Wire the inputs of both instances 
4. Add the distanceBetweeenCoordinates Function from the lambda-distance-demo service 
5. Wire the inputs and output 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step7_duplicateAndWire%20.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%207%20-%20duplicate%20and%20wire%20.gif)

**Step 8:** Test the distanceBetweenAddresses 

1. Click on Top Level PQ and highlight the function 
2. In the right hand panel enter values for origin and target 
   * Origin = “London” 
   * Target = “Birmingham” 
3. Click run 
4. Observe the results in the function results panel. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/videos%202/IntroToKindsAndFunctions_step8_finalTest.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/IntroToKinds/gifs%205/lesson%202%20step%208%20final%20test.gif)



\*\*\*\*

