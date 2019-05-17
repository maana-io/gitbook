# Composing Functions

## What is Function Composition

Function Composition is the process of building up a function's implementation from multiple other functions. This builds up the pipe line used to calculate the final output of the function.

#### Interacting with Functions <a id="FunctionComposition-InteractingwithFunctions"></a>

Interacting with Functions allows you to quickly iterate through a solution. The following describes the functionality to accomplish this.

* Opening the Function Graph for the Function. This allows composing the Function.
* If the Function is composable \(has a Function graph\), the Name shows as a link. Click the name opens the Function Graph. Non-composable Functions include Functions from external services and do not have corresponding function graphs.

**Things to keep in mind when connecting 2 or more function nodes in a function graph**

* An "in" port can only connect to "Output" fields and an "Out" port can only connect to "Input" fields.
* The "out" port from a particular field in the function can go to multiple \(type\) compatible "in" fields of other functions in the function graph. 
* Functions cannot be connected together on a knowledge graph. This must be done only within a function graph.

{% hint style="info" %}
Click and drag from an "out" node to an "in" node to connect two fields from two functions
{% endhint %}

![](../../../../../.gitbook/assets/image%20%2833%29.png)

#### Explorer Panel <a id="FunctionComposition-ExplorerPanel"></a>

The Explorer panel shows the entire hierarchy of Functions. At the root is the top level Function representing the top level PQ. Under it \(when expanding the node in the tree\) are its children. Each child that also has children can be expanded, etc. 

This gives a quick view into the structure of the PQ decomposition. It allows traversing up and down the Function tree without needing to navigate through the graph. Selecting any Function will navigate to its Function graph.

The Function defaults to showing only the first level deep but allows expanding to deeper levels. The Explorer panel does not render the children until expanded to avoid infinite recursion problems.  


![Explorer panel showing the hierarchy for functions](../../../../../.gitbook/assets/image%20%2843%29.png)



