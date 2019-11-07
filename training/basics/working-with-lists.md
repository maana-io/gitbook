# Working with Lists

---------------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [x] Power Point Slides \(**not needed**\)
* [x] Workspaces \([https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases](https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases)\)
* [x] Step-by-Step Instructions for Learning Assistant \(**completed**\)
* [x] Case description \(**completed**\)
* [x] Recording \(**completed\)**
* [x] Gif \(**complete**\)
* [ ] Azure upload \(pending\)
* [ ] Basics Use Case, Workspace, Step by Step, Recordings and gif \(WIP\)

---------------------------------------------------------------------------------------------------------------

## **Intro to Working With Lists**

**Case Description :** While developing solutions, many times we have to perform certain operations such as adding, removing, merging, finding, filtering, reversing, on multiple items. A group of multiple items is called a list or an array. In this exercise we take you through two examples that use Maana Q Scalars in built service to help demonstrate:  1. Combining \(concatenating\) two lists  2. Adding '2' to lists together.  Let's get started!

**Link to Workspace:**

\*\*\*\*[**https://cstrainingstable.knowledge.maana.io/workspace/cdd1250e-191a-4a20-b370-bd1c452beb5f**](https://cstrainingstable.knowledge.maana.io/workspace/cdd1250e-191a-4a20-b370-bd1c452beb5f)\*\*\*\*

**Step by Step Instructions:**

**Step1:** Create a function called  'combineTwoLists' with inputs 'a' of type String list and 'b' of type String list . Make both mandatory by clicking on '!' icon. To create a list, click on 'list' icon. Output is of type String list. Click Save.

**Step2:** Expand on the 'combineTwoLists'  function. Here we will use the Maana Lambda Assistant to implement a function to perform the scalar addition to the list. To do that, search for Maana Lambda Assistant in the search bar. Drag and drop it to the Inventory. Maana Lambda Assistant is now activated in the Assistant panel.

Step 3: Use the following code to implement the function. 



\*\*\*\*

\*\*\*\*

## **Working With Lists Example**

**Case Description:** In this example, we use MaanaQ to aid us in ensuring only those individuals who are above 21 are allowed to enter the MaanaQ bar. This example lets us do just that. In the process, learn how to perform various functions on lists. Use Maana Q to execute functions on multiple items while efficiently caching the result. Maana Q runs the function in parallel using all the available computation resource. We have a list of people and their birthdays. Let's find out who can enter and enjoy the party!

**Link to Workspace:** 

**Step by Step Instructions**

**Step 1:** Create top level function

1. Create a new function and name it "allPeopleOver21". The output type is PersonWith Age and a list \(a.k.a. array\).

**Step2:** Decompose top level function

1. Expand the top level function, "allPeopleOver21". Now we will create several functions. For the first function, look for "allPersons" in the search bar, drag and drop it to the canvas. 

_Note: This function has two inputs "take" and "offset", both INT type. Take is the number of elements to return from the function, and offset is what element to start on. For example, if you have a list \[a,b,c\], take=1, offset=0 will return \[a\]. Another example, in the list \[a,b,c\], take=2, offset=1 will return \[b,c\]._ 

_2._  Next create a function called "getPeopleWithAgeFromPeople". Create an input field called people of type Person and make it a list. The output is a list of type PersonWithAge. Wire the input and output.

3. Next create a function called "filterPeopleOver21". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

4. Next create a function called "filterNullPeopleWithAge". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

**Step3:** Second level of decomposition

1. Expand "getPeopleWithAgeFromPeople", create a function called "getPersonWithAgeFromPerson" with an input called person of type Person. Make this input mandatory by clicking the "!" The output is of type PersonWithAge. Wire the input and output.
2. Go back to the top level decomposition and locate the function called, "filterPeopleOver21". Expand it and create a new function called, "filterPersonIsOver21" with an input called personWithAge of type PersonWithAgeInput. The output is of type PersonWithAge. Wire the input and output.
3. Go back to the top level decomposition and locate the function called, "filterNullPeopleWithAge". Expand it. In the search bar, locate the lambda service called "filterNullPeopleWithAge", drag and drop it to the canvas. Wire the input and output.

**Step4:** Testing

1. Go to the "allPersons" function and run it the context panel on the right side of the screen. Select "input" and expand it. Select take and offset and set both to 0. In the Assistant Panel see the list of all people we are considering. Next go to the top level function called "allPeopleOver21" , run it. A list of those individuals who are 21 or older is returned in the Assistant Panel.

Recordings

[WorkingWithLists\_Step1\_TopPQ](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step1_TopPQ.gif)

[WorkingWithLists\_Step2.1\_allPersons](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.1_allPersons.mov)

[WorkingWithLists\_Step2.2\_getPeopleWithAge\_andWire](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.2_getPeopleWithAge_andWire.mov)

[WorkingWithLists\_Step2.3\_filterPeopleOver21](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.3_filterPeopleOver21.mov)

[WorkingWithLists\_Step2.4\_filterNullPeople](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.4_filterNullPeople.mov)

[WorkingWithLists\_Step3.1\_expand\_getPeopleWithAge](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.1_expand_getPeopleWithAge.mov)

[WorkingWithLists\_Step3.2\_expand\_filterpeopleover21](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.2_expand_filterpeopleover21.mov)

[WorkingWithLists\_Step3.3\_expand\_filterNull](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.3_expand_filterNull.mov)

[WorkingWithLists\_Step4\_Testing](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step4_Testing.mov)



