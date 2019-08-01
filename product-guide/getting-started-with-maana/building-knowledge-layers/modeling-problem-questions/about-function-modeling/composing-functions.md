# Composing Functions

## What is Function Composition

Function Composition is the process of building up a function's implementation from multiple other functions. This is what you will be doing in Q to model your problem-question decomposition. At the same time you are modeling, you are actually creating the solution!

## Function Composition

Let's compose the Functions that make up the solution to the problem-question we created earlier. Note that for the purpose of this tutorial, we have introduced problem-question modeling and Function composition in different sections, however when you are actually developing a solution, these two should be done at the same time.

> PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?

{% hint style="info" %}
Make sure you are familiar with Functions and Kinds before continuing. See [Understanding Kinds](../../kinds-and-functions/) and [Understanding Functions](../../understanding-functions.md).
{% endhint %}

Since the Function composition process should be done at the same time as the problem-question decomposition, we will go through each of the steps we did during problem-question decomposition and show the corresponding Function composition step. For reference, here is the complete problem-question decomposition we came up with before.

> * Top level PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?
>   * PQ: Given an actor and a year, what films was the actor in during the given year?
>     * PQ: Given an actor, what is the list of films the actor was in?
>     * PQ: Given a list of films and a year, what are the films from the list that were released in that year?
>   * PQ: Given a list of films, what is the highest grossing film?

First, let's create our top-level Function. Inside of a Knowledge Graph in our Workspace, click the "Create Function" button.

![Creating the top-level Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Function%20-%20Highest%20Grossing%20Film%20By%20Year.png)

You'll see a new Function has been created and we've given it the name `highestGrossingFilmByYear` . It takes in two inputs, named `actor` and `year` . You will notice that `actor` doesn't have a type yet. We will come back to that in a moment. The type for `year` has been set to INT. Also, in the Information pane of the Context panel on the right, you will see that a description has been added. This will give anyone who looks at this Function a clear idea of what it does.

{% hint style="info" %}
Be sure to click the save button at the top of the Information pane after adding the description.
{% endhint %}

Now back to the `actor` field and its missing type. What should the type be for `actor` ? None of the scalar types \(String, Int, Boolean, Date, etc.\) can be used to uniquely identify an actor. An actor should be comprised of properties like first name, last name, date of birth, films, etc. This means it should be its own type with all of those properties as fields!

If you are working in a common domain in your company, most likely the types you are working with will already exist in either an external service or a Workspace service. \(see [Services](../../../services/) for more details about services\) It is best practice to reuse existing types rather than creating new ones as this will create consistency and it will facilitate interoperability across all of the solutions that are developed in Q.

At the top of the page, search for "actor". \(For more information on searching, see [Searching](../../../searching.md)\)

![Searching for actor Kinds](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Actor%20Search.png)

In the screenshot above, the results show there is an Actor Kind that belongs to a service called Movies. We can click and drag this to our Knowledge Graph to add it to our Workspace and make it available for selection within the type drop down.

![After adding the Actor Kind, it is available for selection in the type drop down](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Actor%20Kind%20Added%20to%20KG%20.png)

Once the Actor Kind has been added to the Knowledge Graph, it shows up in the drop down. Let's go ahead and choose it.

{% hint style="info" %}
If you don't have an Actor Kind from another service as above, you can create one in the Knowledge Graph. We'll do an example of creating a Kind next. See [Inside the Workspace](../../../workspaces/inside-the-workspace.md) for information on creating Kinds.
{% endhint %}

The final part of our Function, that we have up until now ignored, is the `Output`. It defaults to String, but is that what it should be in this case? Just like we have a complex Actor type as an input type we want a complex Film type as the output type. This should come from searching for Film and dragging and dropping the Kind onto our Knowledge Graph. However, for illustration purposes, in this case we will create a new Film Kind.

{% hint style="info" %}
Services can be added to the Workspace inventory for quick access to related types. In this example, we could add the Movies service to our inventory and see all of the Kinds and Functions from the service that are available to us. See [Searching](../../../searching.md) for more details on adding services to the inventory.
{% endhint %}

Click the "Create Kind" button to create a new Kind. Once it shows up, set the name and give it some fields as in the screenshot below.

![Created the Film Kind and added some fields](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Create%20Film%20Kind.png)

You will notice that all of the fields are set as required and the actors field is also set as a list. In addition, the `actors` field type is set to the `Actor` type from the `Movies` service. Note that the `Film` Kind we just created is different from the Kind set as the type for the `films` field in the `Actor` Kind. Normally we would not want to create a new Kind when one already exists as this introduces inconsistency as illustrated above with two different Film types.

Click the Save button to save the Kind and it will become available in the Type drop down for the Function output.

![Film is now available for selection from the Type drop-down in the output](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Film%20in%20Type%20Drop-down.png)

For consistency sake, I am going to remove the `Film` Kind that was just created and use the `Film` Kind from the the `Movies` service. You can continue along with the `Film` and `Actor` Kinds you have created.

Once everything is set in the Function go ahead and save it. Our Knowledge Graph now looks like this.

![The definition of our top-level Function is complete!](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Top%20Level%20Function%20Complete.png)

Now for the next step: composing the `highestGrossingFilmByYear` Function.

### Composing a Function

To be able to compose a Function, we must open the Function composition view, referred to as the Function Graph. To open the Function composition view, click on the expand icon on the Function.

![The expand icon opens the Function Graph](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Open%20Function%20Graph.png)

This will open a new view with Input and Output nodes.

{% hint style="info" %}
Functions from outside of the Workspace \(from outside services\) are not composable or editable, thus you will not see the icons to edit the Function or open the Function Graph.
{% endhint %}

![Inside the Function Graph](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Inside%20the%20Function%20Graph.png)

You will notice that the fields in the Input node match the inputs to the `highestGrossingFilmByYear` Function and that the field in the Output node matches the output. 

{% hint style="info" %}
The Input and Output nodes are not editable. To change the inputs or output, return to the Knowledge Graph containing the Function and edit the Function there. \(You can return to the Knowledge Graph by selecting it in the Explorer panel.\)
{% endhint %}

Now let's review our problem-question decomposition to see how to compose this Function.

> * Top level PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?
>   * PQ: Given an actor and a year, what films was the actor in during the given year?
>     * PQ: Given an actor, what is the list of films the actor was in?
>     * PQ: Given a list of films and a year, what are the films from the list that were released in that year?
>   * PQ: Given a list of films, what is the highest grossing film?

Inside of this Function, there should be two more, corresponding to the two PQs listed underneath the top-level PQ. These can be created using the "Create Function" button, just like in a Knowledge Graph. Let's do that now.

![Composing the top-level Function with two Functions](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Composed%20Highest%20Grossing%20Film.png)

Here we have created `actorsFilmsByYear` to model the first PQ and `highestGrossingFilm` to model the second PQ. The next step is to connect the Functions together to indicate the flow of data. The inputs to `highestGrossingFilmByYear` should go into the inputs of `actorsFilmsByYear` , the output from `actorsFilmsByYear` should go into the input of `highestGrossingFilm` , and the output of `highestGrossingFilm` should go into the output of `highestGrossingFilmByYear` . You can connect these together by clicking on a port and dragging the line to the port it should connect to. \(A line will form as you drag\) Release the mouse over the destination port and the line will change color to indicate a valid connection.

![All of the ports have been connected together](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/All%20Ports%20Connected.png)

Once you are finished, it should look like the screenshot above.

Notice that the Types \(and their modifiers\) of all connected fields are the same. This does not have to be the case. The Q platform will attempt to use connected types even if they are different through a process called "duck typing".  See the "Duck Typing" section below for more details.

{% hint style="info" %}
**Things to keep in mind when connecting Function nodes in a Function Graph**

* An input port can only connect to an output and vice versa.
* The output port from a function can go to multiple input fields of other functions in the function graph. 
* Functions cannot be connected together on a Knowledge Graph. This must be done only within a Function Graph.
{% endhint %}

Now that we have composed the `highestGrossingFilmByYear` Function, there is still one more composition step left:

> * Top level PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?
>   * PQ: Given an actor and a year, what films was the actor in during the given year?
>     * PQ: Given an actor, what is the list of films the actor was in?
>     * PQ: Given a list of films and a year, what are the films from the list that were released in that year?
>   * PQ: Given a list of films, what is the highest grossing film?

We must compose the `actorsFilmsByYear` Function. Once again, we enter its Function Graph view by clicking on the expand icon.

![The Function Graph for actorsFilmsByYear](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Actor%27s%20Films%20By%20Year.png)

Inside of here there are two more Functions to create. Go ahead and create them.

![Composed actorsFilmsByYear](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Actor%27s%20Films%20By%20Year%20Composition.png)

You should end up with what is shown above. Now the composition is complete! \(er... mostly\)

There is one problem with this "solution". It doesn't actually do anything yet! Each of the Functions that do not have a composition \(`actorsFilms`, `filterFilmsByYear`, and `highestGrossingFilm`\) must have code backing them that will perform the intended calculations. These must be implemented in a service \(see [Implementing Services](../../../../reference-guide/q-platform-and-microservices/creating-services/)\). The service then needs to be added to the Q platform \(see [Adding a Service](../../../services/adding-a-service.md)\). Finally, the Functions in the service need to be dragged and dropped from Search into the Function Graph \(just like how Kinds were added to the Knowledge Graph earlier\) and connected together, replacing the Functions that were created above.

The steps for creating a service are outside the scope of this tutorial and require a technical background. Feel free to try them out if you want!

Once that is done, then the Function can be run, and the output analyzed. This can be done in the Q platform as well. We look at that next!

## A Quick Note on the Explorer Panel

The Explorer panel shows the entire hierarchy of Functions. At the root is the top level Function representing the top level PQ. Under it \(when expanding the node in the tree\) are its children. Each child that also has children can be expanded, etc. 

This gives a quick view into the structure of the PQ decomposition. It allows traversing up and down the Function tree without needing to navigate through the graph. Selecting any Function will navigate to its Function graph.

![Example Function Graphs in the Explorer panel](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Function%20Graph%20Explorer%20Panel.png)

The Function Graphs we created for the example in this section will show up as above in the Explorer panel.

## Duck Typing

When connecting an output field with a complex type to an input field with a complex type, the fields in each complex type are matched on name and types. Only fields that can be successfully matched on both will pass their data through. Take for example the following:

![Duck typing example](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Top%20Level%20Function%20Complete.png)

In the screenshot above, we have two Kinds, Actor and Film. Let's say we wanted to connect an output in a Function that has type `Film` to an input field of another Function that has type `Actor` . The Q platform will let us do this, however only matching fields will pass through. Since the only field that matches in both name and type between the two Kinds is `id` that is the only field that would pass its data through successfully. That is probably not what is wanted.

However, in the following example, connecting an output of type Employee to an input of type Person would pass through `firstName`, `lastName`, and `dateOfBirth` fields because they all match on both name and type. The `employer` field would be skipped.

![Kinds matching on multiple fields](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Employee%20Person%20Example.png)





