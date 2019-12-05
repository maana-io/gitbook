# Custom Function using a JavaScript Lambda

To recreate and test this example using your own code, replace Steps 4-7 above with the following:

## Step-by-Step Instructions

_Step 1. Note: If you do not see it in the Assistant Panel, look for it in the search bar and drag it to the inventory. Dragging to the inventory will activate the Maana Lambda Assistant and it will be available in the Assistants Panel_ 

Step 4: Create a function called sayHelloCoded. Create a field called "name" of type STRING. Click save

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_gifs/HelloWorldExtended_Step%204.gif)

[MOV recording](https://maanaimages.blob.core.windows.net/maana-q-documentation/QTraining_videos/HelloWorld_movc/HelloWorldExtended_Step%204.mov)

Step 5: Go to the Assistants panel and switch to Maana Lambda Assistant. In the Assistant Panel, enter the following code:

```javascript
const { name } = input

return `Hello, ${name}`
```

\_\_

Step 6:  Test the function using  the Context Panel 

