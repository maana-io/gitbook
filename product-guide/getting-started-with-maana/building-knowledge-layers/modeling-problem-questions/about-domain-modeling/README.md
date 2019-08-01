# About Domain Modeling

### What is Domain Modeling? <a id="what-is-domain-modeling"></a>

Maana refers to the process of modeling out the concepts of a business problem as Domain Modeling. While Domain Modeling can happen at any point in the process of modeling a solution, this is likely to occur during the process of Function Modeling, as during this process the concepts required for the solution to the problem-questions are determined.

### Domain Modeling in Q

The process of Domain Modeling takes the form of adding Kinds to a Knowledge Graph in Q. The realization of the need for a Kind will often occur during the process of adding inputs to a Function. The types of those inputs may be complex types \(concepts\) which are represented as Kinds in Q. The first choice is to use existing Kinds from existing services. This creates consistency across solutions developed in Q and makes it easier to reuse Functions across solutions. If a particular complex type does not already exist as a Kind in another service, then it may be appropriate to create the Kind in the current service to represent the type. See [Understanding Kinds](../../kinds-and-functions.md) for a description on Kinds and Kind creation.

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

​[  
](https://maana-ue.gitbook.io/product/~/drafts/-LZph7cZfruBt7FBiKE8/primary/product-guide/the-solution-lifecycle/domain-and-function-modeling)

