# Working with Lists

-------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [ ] Azure upload \(pending\)
* [ ] Basics Use Case, Workspace, Step by Step, Recordings and gif \(WIP\)

-------------------------------------------------------------------------------------------------------

## **Part 1: Introduction to Working with Lists**

**Case Description :** While developing solutions, many times we have to perform certain operations such as adding, removing, merging, finding, filtering, reversing, on multiple items. A group of multiple items is called a list or an array. In this exercise we take you through two examples that use Maana Q Scalars in built service to help demonstrate:  1. Combining \(concatenating\) two lists  2. Adding '2' to lists together.  Let's get started!

**Link to Workspace:**

\*\*\*\*[**https://cstrainingstable.knowledge.maana.io/workspace/a1de4fe9-2b69-4108-921c-68b964d53628**](https://cstrainingstable.knowledge.maana.io/workspace/a1de4fe9-2b69-4108-921c-68b964d53628)\*\*\*\*

**Step by Step Instructions:**

**Step1:** Create a function called  'combineTwoLists' with inputs 'a' of type String list and 'b' of type String list . Make both mandatory by clicking on '!' icon. To create a list, click on 'list' icon. Output is of type String list. Click Save.

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Gifs/WorkingWithLists_Intro_Step1.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step1.mov)

![](../../.gitbook/assets/workingwithlists_intro_step1.gif)

**Step2:** Expand on the 'combineTwoLists'  function. Next we will use Maana Q Scalars, a maana pre-built service suite. Search for Maana Q Scalars in the search bar. Drag and drop it to the Inventory. In the Inventory panel, expand Services -&gt;Maana Q Scalars and look for  'StringListConcat'. Drag this to the canvas. Wire the inputs and outputs. 

GIF [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step2.mov)

**Step 3:** Test the function by going to the top level function i.e. 'combineTwoLists'. In the explorer panel, enter in two strings. Click on run. View the function results in the Assistant Panel.

GIF [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Intro/Videos/WorkingWithLists_Intro_Step3.mov)

**Step 4:** In the same knowledge graph, create a new function called 'addTwoToAListOfNumbers' with input called 'listOfNumbers' of type INT list and make it mandatory. The output is a list of type INT. Make it mandatory. Click Save.

**Step 5:** Expand 'addTwoToAListOfNumbers'.  We will use Manna prebuilt services called Constants and Math. So locate these in the search bar. Drag them to the inventory.

**Step 6:** Create a new function here called 'addTwoToNumber' with input called 'number' of type INT. Output is of type INT. Make these mandatory, Click Save. Wire the input and output. 

**Step 7:** Expand the function 'addTwoToNumber'. In the inventory panel, under Services, locate Constants. Expand it and locate the function 'two'. Drag 'two' to the canvas.

**Step 8:** In the inventory panel, under Services, locate Math. Expand it and locate   the function 'intAddition'. Drag 'intAddition' to the canvas.

**Step 9:** Wire inputs and outputs.  There are three wirings - 1. 'Input' function's 'INT' to 'Math:intAddition' function's 'a' 2. 'Constant:two' function's INT to 'Math:intAddition' function's 'b' 3. 'Math:intAddition' function's output INT to the function 'Output'

**Step 10:** Test the function by going to the top level function called 'addTwoToNumber'. In the explorer panel, enter in a list of numbers. Click on run. View the function results in the Assistant Panel.



## **Part 2: Working with Lists Example**

**Case Description:** In this example, we use MaanaQ to aid us in ensuring only those individuals who are above 21 are allowed to enter the MaanaQ bar. This example lets us do just that. In the process, learn how to perform various functions on lists. Use Maana Q to execute functions on multiple items while efficiently caching the result. Maana Q runs the function in parallel using all the available computation resource. We have a list of people and their birthdays. Let's find out who can enter and enjoy the party!

**Link to Workspace:** 

**Step by Step Instructions**

**Step 1:** Create top level function

1. Create a new function and name it "allPeopleOver21". The output type is PersonWith Age and a list \(a.k.a. array\).

WorkingWithLists\_Step1\_TopPQ

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step1_TopPQ.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step1_TopPQ.mov)

![](../../.gitbook/assets/workingwithlists_step1_toppq.gif)

**Step2:** Decompose top level function

1. Expand the top level function, "allPeopleOver21". Now we will create several functions. For the first function, look for "allPersons" in the search bar, drag and drop it to the canvas. 

_Note: This function has two inputs "take" and "offset", both INT type. Take is the number of elements to return from the function, and offset is what element to start on. For example, if you have a list \[a,b,c\], take=1, offset=0 will return \[a\]. Another example, in the list \[a,b,c\], take=2, offset=1 will return \[b,c\]._ 

WorkingWithLists\_Step2.1\_allPersons

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.1_allPersons.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.1_allPersons.mov)

![](../../.gitbook/assets/workingwithlists_step2.1_allpersons.gif)

_2._  Next create a function called "getPeopleWithAgeFromPeople". Create an input field called people of type Person and make it a list. The output is a list of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step2.2\_getPeopleWithAge\_andWire

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.2_getPeopleWithAge_andWire.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.2_getPeopleWithAge_andWire.mov)

![](../../.gitbook/assets/workingwithlists_step2.2_getpeoplewithage_andwire.gif)

3. Next create a function called "filterPeopleOver21". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step2.3\_filterPeopleOver21

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.3_filterPeopleOver21.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.3_filterPeopleOver21.mov)

![](../../.gitbook/assets/workingwithlists_step2.3_filterpeopleover21.gif)

4. Next create a function called "filterNullPeopleWithAge". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step2.4\_filterNullPeople

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.4_filterNullPeople.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.4_filterNullPeople.mov)





**Step3:** Second level of decomposition

1. Expand "getPeopleWithAgeFromPeople", create a function called "getPersonWithAgeFromPerson" with an input called person of type Person. Make this input mandatory by clicking the "!" The output is of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step3.1\_expand\_getPeopleWithAge

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.1_expand_getPeopleWithAge.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.1_expand_getPeopleWithAge.mov)



1. Go back to the top level decomposition and locate the function called, "filterPeopleOver21". Expand it and create a new function called, "filterPersonIsOver21" with an input called personWithAge of type PersonWithAgeInput. The output is of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step3.2\_expand\_filterpeopleover21

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.2_expand_filterpeopleover21.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.2_expand_filterpeopleover21.mov)

1. Go back to the top level decomposition and locate the function called, "filterNullPeopleWithAge". Expand it. In the search bar, locate the lambda service called "filterNullPeopleWithAge", drag and drop it to the canvas. Wire the input and output.

WorkingWithLists\_Step3.3\_expand\_filterNull

[GIF](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.3_expand_filterNull.gif) [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.3_expand_filterNull.mov)

![](../../.gitbook/assets/workingwithlists_step3.3_expand_filternull.gif)

**Step4:** Testing

1. Go to the "allPersons" function and run it the context panel on the right side of the screen. Select "input" and expand it. Select take and offset and set both to 0. In the Assistant Panel see the list of all people we are considering. Next go to the top level function called "allPeopleOver21" , run it. A list of those individuals who are 21 or older is returned in the Assistant Panel.

[WorkingWithLists\_Step4\_Testing](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step4_Testing.mov)

GIF [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step4_Testing.mov)

























