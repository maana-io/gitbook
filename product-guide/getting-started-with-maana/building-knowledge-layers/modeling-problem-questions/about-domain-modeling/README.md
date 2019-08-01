# About Domain Modeling

### What is Domain Modeling? <a id="what-is-domain-modeling"></a>

Maana refers to the process of modeling out the concepts of a business problem as Domain Modeling. While Domain Modeling can happen at any point in the process of modeling a solution, this is likely to occur during the process of Function Modeling, as during this process the concepts required for the solution to the problem-questions are determined.

### Domain Modeling in Q

The process of Domain Modeling takes the form of adding Kinds to a Knowledge Graph in Q. The realization of the need for a Kind will often occur during the process of adding inputs to a Function. The types of those inputs may be complex types \(concepts\) which are represented as Kinds in Q. The first choice is to use existing Kinds from existing services. This creates consistency across solutions developed in Q and makes it easier to reuse Functions across solutions. If a particular complex type does not already exist as a Kind in another service, then it may be appropriate to create the Kind in the current service to represent the type. See [Understanding Kinds](../../kinds-and-functions/) for a description on Kinds and Kind creation.

When creating new Kinds to model a domain, it is incredibly important to communicate and agree on what  fields the Kind should contain across the entire organization. The Kind should be created containing the appropriate fields that make it applicable to _all_ the solutions within the domain it is a part of. Consideration should also be given to what Workspace or service will contain the Kind. Perhaps the Kind is needed for your solution, but it makes sense to create it in another service of related Kinds so other people can easily find it when working on their own solutions. This grouping of related Kinds can help speed up the solution process.

![A domain model representing an expert&apos;s knowledge of a specific domain](https://maanaimages.blob.core.windows.net/maana-q-documentation/well%20interv.png)

{% hint style="info" %}
Key Concepts of Domain Modeling

* Kinds are the concepts \(Nouns\) that are used to solve a problem
* Domain Modeling is the addition of Kinds to the Workspace
* Creation of new Kinds should only happen if an existing Kind corresponding to the concept needed is not available from an existing service
  * If a Kind exists but doesn't have all of the fields needed, an alternative option is to add fields to the Kind
* It is imperative to communicate, agree on, and to map out what fields a Kind contains and what service it should be a part of.
{% endhint %}

## Strategies for Domain Modeling

Sometimes you may not know the exact structure of the concepts involved in the solution that you are creating and it can be distracting to try and search for a Kind that matches what you need while in the middle of Function Modeling. You don't want to be constantly interrupting the Function Modeling flow to find Kinds that match what you need. A strategy that can be used instead is to create a new Kind that has the fields that are needed, use that in the solution initially, and then come back later and replace it with a matching Kind from a service. This has the added benefit of allowing you to modify the Kind as needed during the development of the solution. At the end of modeling the solution, you will have a set of Kinds that reflect exactly what you need, making it easier to find \(or create\) appropriate Kinds in other services to use in the solution instead.

Let's take a look at an example of how this would work. In the example given in [Composing Functions](../about-function-modeling/composing-functions.md), we needed `Actor` and `Film` Kinds for the `highestGrossingFilmByYear` Function. In that example, both Kinds were searched for and found in the Movie service. These were added to the Knowledge Graph and subsequently used within the Function Modeling.

Instead of searching for them, let's follow the strategy above and create them in the Knowledge Graph. 

![Film and Actor Kinds created in the Knowledge Graph](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Domain%20Modeling%20Strategies%20Example.png)

Above, both of the `Actor` and `Film` Kinds were created in the current Workspace and used in the `highestGrossingFilmByYear` Function. During the Function composition process, we can use these Kinds and create additional ones as needed. In this example, these are the only two Kinds.

Now that we are done with Domain Modeling, let's see if we can find Kinds from other services that we can use instead. We want to keep this solution the same Kinds as other solutions for consistency!

![Added two Kinds from the Movies service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Domain%20Modeling%20Strategies%20All%20Kinds.png)

Above, we were able to find two Kinds that have the fields that we need. They have some additional fields compared with the Kinds created in the Workspace but that is fine. 

{% hint style="info" %}
If you are not able to find Kinds that match what you need, it may make more sense to add them to an existing service and import them into this Workspace rather than add them directly to this Workspace. In the case above, we would probably want to add them to a Movies service so that other people can easily find and use them as well.

Likewise, if the Kind is missing fields that are needed for the solution, it may make more sense to modify the Kind and add the fields, rather than create a new Kind.
{% endhint %}

Next, delete the Actor and Film Kinds created in the Workspace. \(click "Delete" on the dialog that pops up\)

![Deleted Actor and Film Kinds](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Domain%20Modeling%20Strategies%20Deleted%20Kinds.png)

Click edit on the `highestGrossingFilmByYear` Function and you will notice that the types of `actor` and `Output` are empty. This is because the Kinds no longer exist! We need to use the Kinds from the Movies service instead.

![Updated to use Kinds from the Movies service](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Domain%20Modeling%20Strategies%20Updated%20Types.png)

Make sure to update all of the Functions in the solution to use the Kinds from the Movie service.

