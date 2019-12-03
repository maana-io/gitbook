---
description: Build your first Maana Q case
---

# Hello, world!

**Case Description:**

This is a hands-on example that will get you started with Maana Q. In this case, learn how to create your own sayHello function, add a function field, and import a service from the inventory to your workspace. Get Maana Q to greet you!

Before you start, please refer to [Workspace](../../product-guide/getting-started-with-maana/workspaces/#what-is-a-workspace) if you do not what this is... 

**Step by Step Instructions:**

1. Once inside your newly created Workspace, create a Knowledge Graph\`

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step1.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step1.gif)

2. In the Knowledge Graph you created, create a function

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step2.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step2.gif)

3. Name the function, "sayHello"

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step3.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step3.gif)

4. Inside the function, create a field called "input" of type string and click save

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step4.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step4.gif)

5. Expand the sayHello function. We will use a pre-existing service called "Greetings" to create a sub function. Go to the search bar and type in Greetings. Drag and drop "Greetings" to Inventory

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step5.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step5.gif)

6. Expand "Greetings" in Inventory to locate the "helloWorld" function. Drag and drop "helloWorld" from Inventory to the Canvas. Wire input and output. sayHello function is now complete.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step6.mov) 

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step6.gif)



7. To test the functionality we just created, locate sayHello function in the Explorer panel and hit Run in the Context Panel . Provide an input. In the Assistant Panel, we see the result.

[MOV](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorld_Step7.mov)

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorld_Step7.gif)



To recreate and test this example using your own code, replace Steps 4-7 above with the following:

Step 4: Create a function called sayHelloCoded. Create a field called "name" of type STRING. Click save

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorldExtended_Step%204.gif)

[MOV recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorldExtended_Step%204.mov)

Step 5: Go to the Assistants panel and switch to Maana Lambda Assistant. In the Assistant Panel, enter the following code:

```text
const {name} = input
return "hello " + name
```

_Note: If you do not see it in the Assistant Panel, look for it in the search bar and drag it to the inventory. Dragging to the inventory will activate the Maana Lambda Assistant and it will be available in the Assistants Panel_ 

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorldExtended_Step5.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorldExtended_Step5.mov)

Step 6:  Test the function using  the Context Panel just like Step 7 above or use GraphiQL to query the function you have just created. To do this, select the Workspace. Switch to  GraphQL IDE in the Assistants. Enter in the following code in the left and run to see the results on the right.

```text
{
  sayHelloCoded (name: "Maana")
}
```

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorldExtended_Step6.gif)

[MOV Recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorldExtended_Step6.mov)

