# Best Practices and Limitations

\[TBD\] @Bryan

## Best Practices <a id="best-practices"></a>

For 3.1.5, you must separate Domain Models from Function Graphs in separate workspaces.  Domain Model types can be referenced in Function Graphs by adding the workspace of the Domain Model to the inventory of a Function Graph.

{% hint style="danger" %}
By not following the above best practice, the workspace will become unusable and will not be able to open.  All work will be lost.
{% endhint %}

## Limitations/Gaps in 3.1.5 \(coming soon\) <a id="limitations-gaps-in-3-1-5-coming-soon"></a>

Known limitations in 3.1.5:

* Tying data from hydrated Kinds to Functions
* Injecting constants into Functions
* In-function ad-hoc script

## Function composition and Name Mangling

GraphQL has two distinct types - InputType and ObjectType. Major differences are:

* ObjectType may have fields of scalar types and **other object types**, it **may have arguments to fields**, and it may have resolvers associated with fields and types
* InputType may have fields of scalar types **and other input types**, **fields may not have parameters and cannot have associated resolvers.**

Currently, both are represented in Q as a single Kind and there's no differentiation between them.

### Post 3.1.5 <a id="post-3-1-5"></a>

* Identify Function PQs.
* Design prototype functions \(including input and output types\) and required services.
* Design and build service endpoints for each service implementation.
* Workaround gaps \(e.g. build service calls to return data or constants\) where possible.

