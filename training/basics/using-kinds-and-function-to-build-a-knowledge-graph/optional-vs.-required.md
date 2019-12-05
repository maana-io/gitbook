# Optional vs. Required

**Use Case Description:** An example to match required and optional inputs/outputs

**Pre-Requisites:**

1. Workspace named `Optional vs. Required` is created
2. Knowledge Graph named `What Happens?` is created
3. `Optional vs Required` Service has been added to the Inventory Panel.  _To do this, search for `Optional vs Required` in the search bar, scroll to Services &gt; Optional vs Required. Drag this to Inventory Panel. You should be able to see a suite of functions  as shown below  which we will use for this exercise._

![](../../../.gitbook/assets/image%20%286%29.png)

**Step by Step Instructions:**

**Step 1:** Create a function called `optional` with field named optional of `String` type. 

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step1.gif)



[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step1.mov) 

**Step 2:** In the same Workspace, create a function called `optionalRequired` with field named optional of `String` type. make the output of type `String` mandatory by clicking on the "!" in the right.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step2.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step2.mov)  

**Step 3:** Create another function called `required` with field name required of type `String`. Make it mandatory. Make the output `string` mandatory too.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step3.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step3.mov)

**Step 4:** Expand the `optional` function using the four square arrows in the right. From the Inventory Panel, drag the \(lambda\) function called  `optional` to the canvas. Wire Input and Output.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step4.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step4.mov)

**Step 5:** Go back to the top layer, expand the `required` function using the four square arrows in the right. From the Inventory Panel, drag the \(lambda\) function called `required` to the canvas. Wire Input and Output.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step5.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step5.mov)

**Step6:** Go back to the top layer, expand the `optionalRequired` function using the four square arrows in the right. Drag the functions you just created called `optional` and `required` to the canvas. Wire Input and Output.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/Gifs/OptionalVsRequired_Step6.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_lessons/OptionalVsRequired/videos/OptionalVsRequired_Step6.mov)

**Step 7**: Test each one of the top level functions by clicking on the desired function and clicking  the `Run` icon in the context panel. The results can be viewed in the Assistant Panel. _**Tip:** Make sure you have Function Result selected in the Assistant Panel to view the test results,_



