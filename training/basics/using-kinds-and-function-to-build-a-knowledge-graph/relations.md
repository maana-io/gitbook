# Relations Between Kinds

Properties are simple, scalar values that describe attributes of a Kind.  Kinds can have relationships with other Kinds, forming a network of connectivity.  As with most things, a balance between conceptual purity and operational pragmatism needs to be struct.  In this lesson, we explore various considerations in modeling relationships between Kinds.

## Step-by-Step Instructions

This lesson continues from the [Functions on Kinds](age.md) lesson, using the same workspace.

**Step 1.**  Create a new Kind `Company`

![](../../../.gitbook/assets/company.png)

In this model, a `Company` has a CEO, which is a `Person`.  Note the line from `Person` slot on `Company` to the `Person` node on the Knowledge Graph canvas.

**Step 2.**  Add a `Company` instance

Relations such as this are internally represented as a **foreign key** reference using the unique identities of the Kind instances.  Thus, when creating an instance of a `Company`, the CEO reference is to its unique id:

![](../../../.gitbook/assets/company-add.png)

**Step 3.** Query your model using Graph_i_QL

In GraphQL, this arrangement allows queries to _flow_ through to the linked data in order to return _hierarchical_ data:

![](../../../.gitbook/assets/company-query.png)

When using function composition, the CKG does not know what fields of a Kind to retrieve or how deep in the hierarchy to go when passing data from boilerplate operations \(i.e., when the data comes from KindDB\).

{% hint style="warning" %}
KindDB will request up-to **8 levels** deep in the hierarchy
{% endhint %}

