# Filtering

  
**Case Description:** In this example, we use MaanaQ to aid us in ensuring only those individuals who are above 21 are allowed to enter the MaanaQ bar. This example lets us do just that. In the process, learn how to perform various functions on lists. Use Maana Q to execute functions on multiple items while efficiently caching the result. Maana Q runs the function in parallel using all the available computation resource. We have a list of people and their birthdays. Let's find out who can enter and enjoy the party!

**Step by Step Instructions**

**Step 1:** Create top level function

1. Create a new function and name it "allPeopleOver21". The output type is PersonWith Age and a list \(a.k.a. array\).

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step1_TopPQ.mov)

![](../../.gitbook/assets/workingwithlists_step1_toppq.gif)

**Step2:** Decompose top level function

1. Expand the top level function, "allPeopleOver21". Now we will create several functions. For the first function, look for "allPersons" in the search bar, drag and drop it to the canvas. 

_Note: This function has two inputs "take" and "offset", both INT type. Take is the number of elements to return from the function, and offset is what element to start on. For example, if you have a list \[a,b,c\], take=1, offset=0 will return \[a\]. Another example, in the list \[a,b,c\], take=2, offset=1 will return \[b,c\]._ 

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.1_allPersons.mov)

![](../../.gitbook/assets/workingwithlists_step2.1_allpersons.gif)

_2._  Next create a function called "getPeopleWithAgeFromPeople". Create an input field called people of type Person and make it a list. The output is a list of type PersonWithAge. Wire the input and output.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.2_getPeopleWithAge_andWire.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.2_getPeopleWithAge_andWire.gif)

3. Next create a function called "filterPeopleOver21". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.3_filterPeopleOver21.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.3_filterPeopleOver21.gif)

4. Next create a function called "filterNullPeopleWithAge". Create an input called peopleWithAge, make it a list. The output is a list of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step2.4\_filterNullPeople

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step2.4_filterNullPeople.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step2.4_filterNullPeople.gif)

**Step3:** Second level of decomposition

1. Expand "getPeopleWithAgeFromPeople", create a function called "getPersonWithAgeFromPerson" with an input called person of type Person. Make this input mandatory by clicking the "!" The output is of type PersonWithAge. Wire the input and output.

WorkingWithLists\_Step3.1\_expand\_getPeopleWithAge

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.1_expand_getPeopleWithAge.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.1_expand_getPeopleWithAge.gif)

2. Go back to the top level decomposition and locate the function called, "filterPeopleOver21". Expand it and create a new function called, "filterPersonIsOver21" with an input called personWithAge of type PersonWithAgeInput. The output is of type PersonWithAge. Wire the input and output.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.2_expand_filterpeopleover21.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.2_expand_filterpeopleover21.gif)

3. Go back to the top level decomposition and locate the function called, "filterNullPeopleWithAge". Expand it. In the search bar, locate the lambda service called "filterNullPeopleWithAge", drag and drop it to the canvas. Wire the input and output.

WorkingWithLists\_Step3.3\_expand\_filterNull

 [MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step3.3_expand_filterNull.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step3.3_expand_filterNull.gif)

**Step4:** Testing

1. Go to the "allPersons" function and run it the context panel on the right side of the screen. Select "input" and expand it. Select take and offset and set both to 0. In the Assistant Panel see the list of all people we are considering. Next go to the top level function called "allPeopleOver21" , run it. A list of those individuals who are 21 or older is returned in the Assistant Panel.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/WorkingWithLists_Step4_Testing.mov)

[https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining\_videos/working\_with\_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists\_Step4\_Testing.gif](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/working_with_lists/Working%20With%20Lists%20Step%20by%20Step/Gifs%206/WorkingWithLists_Step4_Testing.gif) 

  






