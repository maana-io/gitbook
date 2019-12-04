---
description: The essence of the Computational Knowledge Graph
---

# Introduction to Kinds and Functions

## [Kinds](https://app.gitbook.com/@maana/s/q/v/3.2.1/product-guide/reference-guide/technical-design-and-architecture/kinds-and-fields/~/settings/share)

**Kinds** represent a specific interpretation of a concept which have a collection of fields used to describe their attributes. Ex: a kind called ‘City’ may consist of name, latitude, longitude 

Understand more about kinds [here](https://app.gitbook.com/@maana/s/q/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/kinds-and-functions).

### Managed Kinds

Managed Kinds are user-defined Kinds that KindDB provides persistence for. They are called "Managed" Kinds because they are, by default, _managed_ by Maana Q's graph database i.e. they are allocated storage and receive CRUD boilerplate.

Alternatively, a user can "override” Maana Q's persistence for certain Kinds and let Q handle the rest.  This is useful when the instances of the Kinds can be synthesized \(see the [Logical Inference and Semantic Graphs](../../advanced/inference/logical-inference-and-semantic-graphs.md) tutorial for an example of this\).

## [Functions](https://app.gitbook.com/@maana/s/q/~/drafts/-LvBRj60Zf4rtd8JrBE7/v/3.2.1/product-guide/reference-guide/technical-design-and-architecture/function-modeling/create-a-new-function/~/settings/share)

**Functions**  are used to represent problem-questions in Q. Consider, "Given x, what is y?" Functions allow you to define x and y and break the problem down further \(decompose it\) into smaller pieces. The Q UI allows connecting Functions together in meaningful ways to form the computational portion of your solutions. Functions are representations of GraphQL queries and mutations.

Understand more about functions [here](https://app.gitbook.com/@maana/s/q/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/understanding-functions).

### GraphQL Query vs. Mutation

A **Query** is performed when it is required to get some information from the knowledge graph.  These operations will be cached by CKG for efficient operation.

More about a graph query can be found [here](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/technical-design-and-architecture/kinds-and-fields/kind-queries)

A **Mutation** is done when it is required to change some information in the graph.  These operations will **not** be cached by CKG, since they are expected to produce "[side-effects](https://en.wikipedia.org/wiki/Side_effect_%28computer_science%29)."

More about a graph mutation can be found [here](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/graphql/graphql-schema-language/graph-mutations)

## [Auto-Generated Kinds and Functions](https://maana.gitbook.io/q/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/kinds-and-functions/auto-generated-kinds-and-functions) \(aka "Boilerplate"\)

Learn more [here](https://maana.gitbook.io/q/v/3.2.1/product-guide/getting-started-with-maana/building-knowledge-layers/kinds-and-functions/auto-generated-kinds-and-functions)

### CRUD Operations

The common set of data operations are: Create, Read, Update, and Delete, or CRUD.  For Managed Kinds, Maana Q automatically generates a set of queries and mutations.  Let's use the example Kind `Person`:

* `person(id: ID!): Person` - this _read_ query will attempt to retrieve a specific `Person` instance by unique identifier.  If none is found, then `null` will be returned.
* `persons(ids: [ID!]): [Person]` - this _read_ query will attempt to retrieve a collection of `Person` instance by their unique identifiers. Missing elements will contain null values.  Values in the return are ordered the same as the input identifiers. \(Note the simple pluralization of simply adding an 's' to the end of the Kind name.\)
* `allPersons(take: INT, offset: INT): [Person!]!` - a _read_ query that will attempt to retrieve all of the Person instances.  Since this could exceed the transmission limits of the HTTP/JSON connection \(max ~500mb\), **paging** is provided using the `take` and `offset` optional arguments. To get the first 1000, call `allPersons(take: 1000, offset: 0)`  and simply increment the `offset` by the `take` to get paging behavior.
* `addPerson(input: AddPersonInput!): ID` - this _create_ mutation creates a new `Person` instance \(or updates an existing one, i.e., _upsert_\) and returns its unique identity, if successful.
* `updatePerson(input: AddPersonInput!): ID` - this _update_ mutation does what it advertises: updates an existing instance of `Person`.
* `deletePerson(id: ID!): Person` - this _delete_ mutation will delete the `Person` instance, if it exists, returning the full instance to the caller.

### Query and Filter Boilerplate

In addition to the standard CRUD operations, Maana Q also generates several queries that are useful for, well, querying the KindDB graph database.

{% hint style="info" %}
Search, advanced query, and filter operations are only available for KindDB-based services.
{% endhint %}

* `Query` - this function allows you to specify complex join, conditional operators, and result shaping to produce an arbitrary set of result data.  While powerful, it does not produce native GraphQL datatypes, but rather JSON.
* `Filter` - each Kind also has a strongly-typed function that can be used to efficiently apply to instances of a Kind using the same powerful conditional operators as full-blown `Query`.

