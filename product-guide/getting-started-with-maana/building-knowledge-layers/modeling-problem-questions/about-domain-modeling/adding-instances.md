# Adding Instances

Adding Instances to a Kind can be useful for testing the output of Functions that have a Kind as the type for one or more input fields. This allows specific scenarios to be repeatedly tested more easily as the Instance can contain all of the test data. The Run pane will be auto-populated with the values for the Instance when it is selected \(See Selecting an Instance in [Running Functions](../about-function-modeling/running-functions.md)\) so they do not need to be manually entered.

If you followed the strategy outlined in [About Domain Modeling](./), you will have created one or more Kinds in your Knowledge Graph that are used in the Functions. Let's take the example that was presented there.

![Domain Model with Actor and Film Kinds](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Domain%20Modeling%20Strategies%20Example.png)

Let's add an instance of `Actor`. There are two ways of doing this, one using the auto-generated Functions, and the other using the Workspace GraphQL IDE Assistant.

### Adding Instances using Auto-Generated Functions

{% hint style="info" %}
For an explanation of what Auto-Generated Function are, see [Auto-Generated Kinds and Functions](../../kinds-and-functions/auto-generated-kinds-and-functions.md).
{% endhint %}

In the Workspace Inventory search for "addFilm". Under Functions -&gt; Auto-Generated select the `addFilm` Function.

![Selected the addFilm Function in the Inventory](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/addFilm%20Instance%20Run%20Pane.png)

In the Run pane of the Context Panel, expand the input type. Here you can enter values for an Instance of the Film Kind \(make sure to check the box next to input!\). When the Run button is clicked, it will add the Instance.

![Enter some values for addFilm](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Entered%20Values%20for%20addFilm.png)

After clicking the Run button, you will see a response in the Function Results Assistant with the result \(just the ID of the Film that was added\).

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/addFilm%20Results.png)

Now, select the Film Kind.

![](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Selected%20Film%20Kind%20after%20addFilm.png)

You will notice in the Data View Assistant that there is now the Instance that we added!

{% hint style="info" %}
When adding an Instance of a Kind that has a field of a complex type \(another Kind\), the value for that field should be the ID of the Instance in the other Kind.
{% endhint %}

This instance can now be selected from the Select Instance dialog when running a Function.

### Adding Instances using the GraphQL IDE Assistant

Selecting the Workspace in the Explorer panel will open the GraphQL IDE Assistant. In this Assistant, you can compose GraphQL queries and mutations and run them. So alternatively use the Run pane, you can compose the mutation in the GraphQL IDE Assistant using the same `addFilm` Function. \(There is also `addFilms` for adding multiple at a time.\)

![Adding a film via the GraphQL IDE Assistant](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/addFilm%20GraphQL%20IDE%20Assistant.png)

When running this you will see the result on the right. Click on the Film Kind again and the new Instance will show up in the Data View Assistant.

![The Instance was added to the Film Kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Selected%20Film%20Kind%20after%20addFilm2.png)



