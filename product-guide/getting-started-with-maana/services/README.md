# Services

## What is a service?

Eventually, the solution that is built needs to actually call out to Functions that execute code to do something. Where do these Functions come from? They come from services!

Simplistically speaking, a service just exposes Kinds and/or Functions through GraphQL that can be used in a Workspace to create a solution. This introduces a very powerful concept. This allows \(and highly encourages\) the reuse of Kinds and Functions when building solutions in Workspaces.

![The &quot;Maana Named Entity Recognition&quot; service in the Workspace Inventory](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Inventory%20Service%20Example.png)

## The importance of reusing Kinds and Functions

So you may ask, why reuse Kinds and Functions? It reduces the code needing to be implemented and maintained for a solution, and it also promotes consistency across solutions. For example, if you need a Function that adds two numbers together, a new Function could be implemented that does this. However, most likely someone else has already needed the same functionality and it exists in a Function somewhere that you can use in your solution. Why reinvent the wheel?

Similarly for Kinds, let's say you need a Person Kind that has name, age, etc. You could create a new Kind in your Workspace and use that within the Functions that you create. However, someone else has probably needed a Person Kind before as well. Reusing an existing Person Kind instead of creating a new one guarantees compatibility between the Functions you create that use the Person Kind and Functions created by other people that also use the Person Kind.  The Functions will "speak the same language".

