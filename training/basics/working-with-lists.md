# Working with lists

---------------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [x] Power Point Slides \(**not needed**\)
* [x] Workspaces \([https://lastknowngood.knowledge.maana.io/workspace/d5a3e4bd-3a8a-46cb-a06e-a96539cc6359 ](https://lastknowngood.knowledge.maana.io/workspace/d5a3e4bd-3a8a-46cb-a06e-a96539cc6359%20)\)
* [x] Step-by-Step Instructions for Learning Assistant \(**completed**\)
* [x] Case description \(**completed**\)
* [x] Recording \(**completed\)**
* [ ] Gif \(**pending**\)

---------------------------------------------------------------------------------------------------------------

**Link to Workspace:** [**https://lastknowngood.knowledge.maana.io/workspace/5df7b12c-98bf-4093-a6a7-49417669241b**](https://lastknowngood.knowledge.maana.io/workspace/5df7b12c-98bf-4093-a6a7-49417669241b)\*\*\*\*

**Case Description:**

In this example, we use MaanaQ to aid us in ensuring only those individuals who are above 21 are allowed to enter the MaanaQ bar. This example lets us do just that. In the process, learn how to work with lists. While developing solutions, many times we have to perform certain operations such as adding, removing, merging, finding, filtering, reversing, on multiple items. In this use case use Maana Q to execute functions such as on multiple items while efficiently caching the result. Maana Q runs the function in parallel using all the available computation resource. We have a list of people and their birthdays. Let's find out who can enter and enjoy the party!

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

