# Understanding Functions

## Understanding Maana Functions

Functions are used to represent problem-questions in Q. Remember the example of "Given x, what is y"? Functions allow you to define x and y and break the problem down further \(decompose it\) into smaller pieces. The Q UI allows connecting Functions together in meaningful ways to form the computational portion of your solutions. Functions are representations of GraphQL queries and mutations.

Functions in Maana fall into two general categories

1. **Authored functions** 
2. **Imported functions**

### Authored Functions

These are created by you by clicking on the "New Function" icon in any Knowledge or Function Graph within a workspace. 

These allow you to author the schema \(inputs and output\) and the implementation of the Function.

{% hint style="info" %}
Authored Functions become GraphQL queries in the Workspace service.
{% endhint %}

![Example of an authored Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Manually%20Created%20Function.png)

### Imported Functions

Services that have a GraphQL endpoint will likely have queries and mutations. When the service is added to Q these will be represented as Functions. The Function names will be preceded with the service name to help disambiguate same named Functions from different services.

Running these Functions will run the backing query or mutation from the GraphQL service.

![Imported &quot;extract&quot; Function from the &quot;Maana Named Entity Recognition&quot; service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Imported%20Function.png)

{% hint style="info" %}
Imported Functions are not editable in Q.
{% endhint %}

### The Structure of a Function <a id="the-structure-of-a-kind"></a>

The screenshot below shows the structure of a function

![Structure of a Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Anatomy%20of%20a%20Function.png)

Let's go through each of the different parts of the Kind node in more detail.

#### Input Fields

The input fields of a Function represent the input that is expected to a Function. The Field column has the name of the field and the Type column has the type \(including modifiers\) that is expected as input to that field.

There are also two modifiers indicated in the Type column: required and list. If the Type has an exclamation mark \(**!**\), the field is required to have a value. If the Type is surrounded in square brackets \(**\[\]**\), the field value is a list. Note that both can be present. Thus **\[STRING!\]!** means the field requires a list of Strings to be provided, where each value in the list cannot be null and the list itself must not be null.

#### Output Field

The output field represents the expected output from a Function. Only the type is editable on the output field and there is only one output. The output field type has the same modifiers as the input fields. In the screenshot above, the output is a String.

{% hint style="info" %}
You will notice that the Function node only has ports on the left side of the inputs and on the right side of the output. This is to indicate the flow of data through the Function from left to right. Data can only go "in" to inputs and "out" of the output. The use of these ports is described in more detail in the [Composing Functions](modeling-problem-questions/about-function-modeling/composing-functions.md) section.
{% endhint %}

### In-node Editing

Like Kinds, Functions can also be edited via in-node editing. To enter in-node editing, click the pencil icon in the top right corner. \(An alternative way to enter edit mode is to double click on the node.\)

![Function in edit mode](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/In-node%20Editing%20-%20Function.png)

{% hint style="info" %}
You can only edit Function nodes that were created in the currently open Workspace.
{% endhint %}

Here you can change the name of the Function, the name of the input fields, the types of the fields, and the modifiers applied to each field. The first two buttons to the right of the type column toggle the required and list modifiers on the field, respectively. You can also add or remove input fields from the Function. Clicking the Save button will save any modifications. Clicking the Cancel button will discard the changes.

{% hint style="warning" %}
Changing the fields of a Function will affect anywhere that references the Function. This could potentially cause problems in the places that use the Function \(such as in the composition of other Functions\).
{% endhint %}

### Editing in the Context Panel

The Information pane of the Context panel allows viewing and editing some additional properties of the Function.

![The Information pane of a Function](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Information%20Pane%20-%20Function.png)

The following properties are editable:

* **name:** The name of the Function. This is the same name when editing in-node.
* **description:** Use this to provide more information about the Function that would help someone else understand what the Function does \(such as the problem-question it solves\). \(The description is only shown in this location in the UI\)
* **graphqlOperationType**: This is where you can change whether this Function is a GraphQL query or mutation within the Workspace service. The default is query.

The un-editable properties include:

* **id**: the ID of the Function

The Information pane also includes a quick view of the schema of the Function, similar to what you would see in the Function node on the graph.

