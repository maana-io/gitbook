# Running Functions

## How to Run Functions

During the Function composition process, you may want to test that Functions are returning values that you expect when they are run. The Q platform provides a way to run a Function with user provided values and see the results of the calculations.

In the following example, a Function has been created called `intToTheFourthPower` that is constructed by calling the `intSquare` Function from the Math service twice.

![The Function Graph for intToTheFourthPower](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Function%20IntToTheFourthPower.png)

Perhaps we want to test that `intSquare` is actually returning an integer multiplied by itself. We can do this by selecting the Function and opening the Run pane in the Context panel.

![Opening the Run pane for the intSquare Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/intSquare%20Run%20Pane.png)

In the Run pane there is a single field. It contains the placeholder text `i INT` which means that the field corresponds to the input field named `i` in the `intSquare` Function and that the input type is `INT`. Let's enter a value into the field and click the Run button.

![After running the intSquare Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Running%20the%20intSquare%20Function.png)

If you were running a Function yourself, you would notice a few things happen. When entering a value in the textbox, the checkbox next to it becomes checked automatically. The checkbox determines whether the value in the field is sent.

The next noticeable thing is that the Run button becomes momentarily disabled after clicking it. This indicates that the Function is being executed. Once it finishes the Run button becomes enabled again.

Finally, the results of running the Function appear in the Function Results Assistant in the Assistants pane. In the example above, we can see that the intSquare Function did indeed multiply the input by itself as we expected.

Now let's return to the Knowledge Graph where the `intToTheFourthPower` Function was created. We can execute the Function from there.

{% hint style="info" %}
A Function must be selected in a Knowledge Graph, Function Graph, or within the Workspace inventory to be able to be run.
{% endhint %}

![Running the intToTheFourthPower Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Running%20the%20intToTheFourthPower%20Function.png)

From within the Knowledge Graph, we can run the `intToTheFourthPower` Function that we just created. As can be seen in the screenshot above it produces the expected results!

You can see that being able to run a Function can be extremely helpful, especially when creating complex solutions. Now that we've taken a look at a simple example, let's take a look at a more complex example to highlight the additional capabilities of the Run pane.

## Running a complex Function

Let's take a look at the Function that was created in the previous section, [Composing Functions](composing-functions.md). There we created a Function called `highestGrossingFilmByYear`. Select it in the the Knowledge Graph, and open the Run pane.

![The Run pane for highestGrossingFilmByYear](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Run%20Pane%20highestGrossingFilmByYear.png)

Here we see two inputs corresponding to the two inputs of the Function. The first thing to notice is the asterisk next to the two fields in the Run pane. This indicates that the fields are required to have a value provided. The second thing that really sticks out is the `actor` field has an arrow next to its checkbox and a "Select Instance" button on the right. This is how a field is displayed when the type is a complex type \(in this case `Actor`\). Clicking the arrow next to the checkbox will expand it to display its fields.

![Expanded actor field](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Expanded%20Actor%20Field%20highestGrossingFilmByYear.png)

We can see all of the fields in the actor input field. We can manually enter values for each of the fields in order to run the Function.

![Manually entering values for the actor fields](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Manually%20Entered%20Values%20highestGrossingFilmByYear.png)

{% hint style="info" %}
The checkbox next to `actor` must be manually checked in order to send the data that was entered for the actor.
{% endhint %}

Here we have entered values for all of the required fields and checked the checkbox next to `actor` so that they will be sent when running the Function. The `films` field is itself a complex type within the `Actor` type. Just like with the `actor` field this can be expanded as well to show its fields.

{% hint style="info" %}
Fields within a type are indented underneath the type in the Run pane.
{% endhint %}

There is one additional option. The "Select Instance" button. If the type that is expected as input to the field has Instances in the Q platform, this button can be used to select one of the Instances and it will auto populate the field values from that Instance.

Let's try selecting an Instance.

{% hint style="info" %}
Selecting an Instance requires the Kinds to have Instances. See [Adding Instances ](../about-domain-modeling/adding-instances.md)for how this is done.
{% endhint %}

### Selecting an Instance

Clicking the "Select Instance" button opens a dialog that allows choosing the Instance.

![Select Instance dialog](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Select%20Instance%20Dialog.png)

The Service field allows changing the Service that the Kind field is populated from. It defaults to the current Workspace. Only Kinds available in that Service are available for selection in the Kind field. The Kind field allows choosing the Kind whose Instances are shown in the Instances table. The Kind defaults to the Kind that corresponds to the type expected by the field in the Function. In this case it is `Actor` so that is the default selected Kind. The Actor Kind includes two Instances in the screenshot above.

The dialog also allows filtering the Instances \(as sometimes there can be a lot!\). To apply filters, click the arrow next to the `id` field.

![Select Instance dialog with filters showing](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Select%20Instance%20Dialog%20with%20Filters%20Showing.png)

Text can be entered into the textboxes above the fields and when the filters are applied, only those Instances with values in the field matching the text will be shown.

![Select Instance Dialog with filters applied](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Select%20Instance%20Dialog%20Filters%20Applied.png)

Above, a filter on the `lastName` field with the value "Ford" has been applied. To remove the filter, click the red X next to the value that will show up when hovering the mouse over the filter.

Let's choose "Harrison Ford" by selecting the radio button on the left and click OK.

![Values are auto populated from the Select Instance dialog](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/highestGrossingFilmByYear%20Select%20Instance%20Populated.png)

The values are auto-populated from the Instance!

{% hint style="info" %}
An Instance from _any_ Kind can be selected in the Select Instance dialog. It doesn't have to be the Kind corresponding to the type of the field in the Function. If an Instance from a different Kind is selected, the Q platform will match the fields in the selected Instance with the fields expected by the field in the Function based on name. For example, if the selected instance has a field named `firstName`, the value from that field will be used in the `firstName` field of the `actor` field.
{% endhint %}

### Entering Lists of Values

Lists of values are supported for scalar types. The ability to enter lists of complex types is coming in the future.

![Example of a list field](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/List%20of%20Values%20highestGrossingFilmByYear.png)

In the example above, the `year` field has been changed to `years` and set to take a list of values. In the Run pane the type is surrounded in `[]` to indicate that it is a list field. Lists of values can be entered by separating the values with commas.

![Example list of values](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Entering%20a%20List%20of%20Values.png)

{% hint style="info" %}
A Function containing a field that has a list of a complex type \(such as Actor\) can still be run, however only a single value for the complex type list is currently supported. The field is displayed the same as a field that is a single complex type \(non-list\) in the Run pane, and when running the Function is sent as the only value in the list.
{% endhint %}

## Errors

If there is an error when running the Function, the error is displayed \(along with any partial results\) in the Function Results Assistant.

![Errors are displayed in the Function Results Assistant](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Errors%20When%20Running%20Functions.png)

The errors are shown underneath the "errors" node.

