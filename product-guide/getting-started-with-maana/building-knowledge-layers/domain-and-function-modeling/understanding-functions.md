# Understanding Functions

## Understanding Maana Functions

Functions are the term that Maana uses for the problem-question used to build their Knowledge Graphs. Remember the example of "Given x, what is y"? These functions allow you to define x and y and connect them to other functions in meaningful ways to form the computational portion of your solutions and your knowledge graph. In graphQL speak, functions are either queries or mutations.

Functions in Maana fall into two general categories

1. **Authored functions** 
2. **Imported functions**

### Authored Functions

These are created by you by clicking on the "sigma" icon in any knowledge or function graph within a workspace. 

You can edit the schema \(including field modifiers\) of these functions at any given time, although there may be consequences depending on what else they are connected to. 

You can also define the implementation of these functions by clicking through the name of the function which is also a hyperlink and opening its function graph.

### Imported Functions

These are queries or mutations that authors of a service \(accessed via a graphQL endpoint\) have made available for others \(like yourself\) to leverage. 

It's important to note that though these can be incredibly useful in building out your solution, you _cannot_ edit the schema or the implementation \(underlying logic\) of these functions.

### The Structure of a Function <a id="the-structure-of-a-kind"></a>

The screenshot below shows the anatomy of a function

![Function node](https://maanaimages.blob.core.windows.net/maana-q-documentation/n1.png)

Like Kinds, Functions can also be edited via in-node editing \(see screenshot below\)

![Double click on node to enable in-node editing](https://maanaimages.blob.core.windows.net/maana-q-documentation/n2.png)

However, by selecting the function and clicking on the info \(i\) tab in the context panel, you won't be able to edit the schema or field modifiers \(list or mandatory\). Here you will be able to access the id for the function and modify the function name, description and graphqlOperationType \(Query or Mutation\). 

![Function options through the info tab in the context panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/n3.png)

### Field Modifiers

There are two field level modifiers available in Maana functions

1. List - indicates that the field is a list of values
2. Mandatory - indicates that the field is _required_ for the function to execute 

