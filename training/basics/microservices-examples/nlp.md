---
description: Natural Language Processing
---

# NLP

Presenter: ****Mike Crooks

**Use Case Description:**  

Important and useful information could be located within written documents and as part of a solution the need to extract key entities from these documents is required.  This example demonstrates how the Maana Q platform can be utilized to extract key “entities”, in this case People, Places and Organizations from raw, inputted text.  

Given the following sentence, “Mike lives in London and has just started working for Maana Inc” we expect the system to extract “Mike”, “London” and “Maana Inc” representing the people, places and organizations.  

**Step by Step Instructions:** 

**Step 1:** Create new workspace and rename 

1. Click on the + icon in the workspace tab, on the left hand side 
2. In the workspace details panel give the workspace a new name -&gt; “Simple NLP Engine” 
3. Click the save icon  



**Step 2:** Create “top level” function 

1. Above the canvas click on the create function button, a green function box will appear.  
2. Give the function a name e.g “extractPeoplePlacesOrganizationsFromDocuments”.  Ensure that you use the camelCase naming convention to differentiate between functions and kinds.  A function requires inputs and outputs to be defined.   
3. Add an input by clicking on the line below the “field” heading and type “documents”.  The input to this function will be a list of string values that represents the text to perform the extraction on.  A field requires a type and this will be STRING.   
4. Click on the line below the “Value” heading and type STRING or select STRING from the drop down menu.  
5. In addition, click the ! icon and the list icon next to it.  This indicates that the field document is required and there will be a list of STRINGS supplied as the input. 
6. Specify the output which again is a list of Strings.  Ensure that that the ! Icon is selected and also the list icon since the aim is to obtain a list of entities in the output. 
7. Click Save 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step1_topLevelFunction.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step1Step_createTopLevelFunction.gif)

**Step 3:** Open the Function Graph and import services to be used 

1. In the search bar in the top menu, search for “maana-natural-compromise”, when the search has completed select services and scroll to find the maana-natural-compromise service.
2. Select this service and drag into the inventory panel located in the bottom left of the screen.

You have now added the maana-natual-compromise service to your workspace.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step2_functionGraphAndImportingServices.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step3_serviceFunctionsAndWiring.gif)

**Step 4: Import "maana Q Scalars" Service**

1. In the search bar in the top menu, search for “Maana Q Scalars”, when the search has completed select services and scroll to find the maana Q Scalars service.
2. Select this service and drag into the inventory panel located in the bottom left of the screen.

You have now added the "Maana Q Scalars" service to your workspace.

**Step 5:** **Expand the function**

Click on the 4 arrows located in the top right hand corner of the function box. This will take us to a canvas where we can begin to “wire up” our function

**Step 6: Add people, places and organizations functions**

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step2_%20functionGraphAndImportingServices.gif)

**Step 7: Add stringListunion functions**

1. Locate the stringListUnion function within the maana Q Scalars service and drag onto the canvas. b 2.Repeat for a second stringListUnion function.

**Step 8: Wire the functions**

1. To wire the functions up click on the right hand box of the input box.
2. Drag the “wire” to the input box of the organizations function.

The inputs are always on the left of a function box with outputs on the right.

3.Repeat this step for the other 2 functions, people and places. 4.To wire up the first union function click on the output of organizations and wire to the first union function. 5.Repeat this for the people function.  
6.The places function is to be wired to the second union function along with the output of the first union function 7.Click on the output box of the second union function and wire to the output box.

\*\*\*\*

\*\*\*\*

\*\*\*\*

