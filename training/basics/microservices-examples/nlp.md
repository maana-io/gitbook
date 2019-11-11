---
description: Natural Language Processing
---

# NLP

Presenter: ****Mike

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

![](../../../.gitbook/assets/nlp_step1step_createtoplevelfunction.gif)

**Step 3:** Open the Function Graph and import services to be used 

1. Click on the 4 arrows located in the top right hand corner of the function box. This will take us to a canvas where we can begin to “wire up” our function. _Note that the search bar struggles to find manna-natural-compromise so it is required to search only for maana and then scroll._ 
2. In the search bar in the top menu type “maana”, when the search has completed select services and scroll to find the maana-natural-compromise service.   
3. Select this service and drag into the inventory panel located in the bottom left of the screen.  You have now added the maana-natual-compromise service to your workspace.   
4. Repeat this process for the maana-utilities service. Services contain a collection of functions that we can use in our use case.  In this case we will use the following functions from the services; 

Maana-natural-compromise -&gt; people, organizations, places  

Maana-utilities -&gt; union 

To explore what functions are available you can click on the arrow next to the Services in the inventory panel and continue down to see what functions are available. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step2_functionGraphAndImportingServices.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step2_%20functionGraphAndImportingServices.gif)

**Step 4:** Add the People, places and Organizations functions and wire them up.

1. Ensure you are in the input / output canvas for the extractPeoplePlacesOrganizations function 
2. Select the People function from the maana-natural-compromise service and drag it onto the canvas.   
3. Repeat this for the Places and Organizations functions. 
4. To wire the functions up click on the right hand box of the input box.   
5. Drag the “wire” to the input box of the organizations function.  The inputs are always on the left of a function box with outputs on the right. 
6. . Repeat this step for the other 2 functions, people and places. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step3_serviceFunctionsAndWiring.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step3_serviceFunctionsAndWiring.gif)

**Step 5:** Add the union function and wire them up! 

Since we have 3 functions that have 3 separate outputs we need to aggregate these into a single list.  The union function allows us to achieve this but since the union function only accepts 2 lists we will need 2 union functions to produce our single list.  

1. Locate the union function within the maana-utiliites service and drag onto the canvas.  
2. Repeat for a second union function. 
3. To wire up the first union function click on the output of organizations and wire to the first union function.  
4. Repeat this for the people function.   
5. The places function is to be wired to the second union function along with the output of the first union function. 
6. Click on the output box of the second union function and wire to the output box. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step4_unionWiringToOutput.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step4_UnionWiringToOutput.gif)



**Step 6:** Test the top level function and examine the output 

1. Click on “New Knowledge Graph” in the top left panel to return to the top canvas where our Top level function resides. 
2. Click on the extractPeoplePlacesOrganizationsFromDocuments function box to highlight it 
3. In the details panel on the right hand side click the “play” icon 
4. Click the check box and paste the following text next to it; 
5. “Mike lives in London and has just started working for Maana Inc” 
6. Click Run. Below the main canvas you will see an “assistants” panel \(expand it if it is not visible\). The functions outputs will be displayed here if the function ran successfully 
7. Expand the arrows until you see the data that has been returned. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/Videos%206/NLP_step5_testing.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/nlp_gifs/gifs%207/NLP_step5_testing.gif)

