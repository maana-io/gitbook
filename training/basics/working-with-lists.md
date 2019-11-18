---
description: Execute functions efficiently using Maana Q
---

# Working with Lists

**Case Description :** While developing solutions, many times we have to perform certain operations such as adding, removing, merging, finding, filtering, reversing, on multiple items. A group of multiple items is called a list or an array. In this exercise we take you through two examples that use Maana Q Scalars in built service to help demonstrate:  1. Combining \(concatenating\) two lists  2. Adding '2' to list a.  Let's get started!

**Link to Workspace:**

\*\*\*\*[**https://cstrainingstable.knowledge.maana.io/workspace/a1de4fe9-2b69-4108-921c-68b964d53628**](https://cstrainingstable.knowledge.maana.io/workspace/a1de4fe9-2b69-4108-921c-68b964d53628)\*\*\*\*

**Step by Step Instructions:**

**Step1:** Create a function called  'combineTwoLists' with inputs 'a' of type String list and 'b' of type String list . Make both mandatory by clicking on '!' icon. To create a list, click on 'list' icon. Output is of type String list. Click Save.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step1.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step1.gif)

**Step2:** Expand on the 'combineTwoLists'  function. Next we will use Maana Q Scalars, a maana pre-built service suite. Search for Maana Q Scalars in the search bar. Drag and drop it to the Inventory. In the Inventory panel, expand Services -&gt;Maana Q Scalars and look for  'StringListConcat'. Drag this to the canvas. Wire the inputs and outputs. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step2.mov)  
[https://maanaimages.blob.core.windows.net/maana-q- Zx](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step2.gif)Adding, removing, merging, finding, filtering, reversing, map/reducing, ...[documentation/QTraining\_videos/working\_with\_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists\_Intro\_Step2.gif](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step2.gif) 



**Step 3:** Test the function by going to the top level function i.e. 'combineTwoLists'. In the explorer panel, enter in two strings. Click on run. View the function results in the Assistant Panel.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step3.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step3.gif)



**Step 4:** In the same knowledge graph, create a new function called 'addTwoToAListOfNumbers' with input called 'listOfNumbers' of type INT list and make it mandatory. The output is a list of type INT. Make it mandatory. Click Save.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step4.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step4.gif)



**Step 5:** Expand 'addTwoToAListOfNumbers'.  We will use Manna prebuilt services called Constants and Math. So locate these in the search bar. Drag them to the inventory.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step5.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step5.gif)



**Step 6:** Create a new function under expansion of 'addTwoToAListOfNumbers' called 'addTwoToNumber' with input called 'number' of type INT. Output is of type INT. Make these mandatory, Click Save. Wire the input and output. 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step6.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step6.gif)



**Step 7:** Expand the function 'addTwoToNumber'. In the inventory panel, under Services, locate Constants. Expand it and locate the function 'two'. Drag 'two' to the canvas.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step7.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step7.gif)



**Step 8:** In the inventory panel, under Services, locate Math. Expand it and locate   the function 'intAddition'. Drag 'intAddition' to the canvas.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step8.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step8.gif)



**Step 9:** Wire inputs and outputs.  There are three wirings - 1. 'Input' function's 'INT' to 'Math:intAddition' function's 'a' 2. 'Constant:two' function's INT to 'Math:intAddition' function's 'b' 3. 'Math:intAddition' function's output INT to the function 'Output'

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step9.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step9.gif)



**Step 10:** Test the function by going to the top level function called 'addTwoToNumber'. In the explorer panel, enter in a list of numbers. Click on run. View the function results in the Assistant Panel.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step10.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step10.gif)





## 





















