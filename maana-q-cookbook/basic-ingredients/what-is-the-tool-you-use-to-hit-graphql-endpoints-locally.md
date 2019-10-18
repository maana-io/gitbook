# What is the tool you use to hit GraphQL endpoints locally?

## Question

#### What is the tool you use to hit GraphQL endpoints locally?

What is the best GraphQL IDE, something with more features than GraphIQL?

## Answers

{% tabs %}
{% tab title="Altair" %}
Altair is the most fully-featured IDE, complete with saved histories, headers, subscriptions, etc. It is also cross-platform and includes a Chrome extension. [https://altair.sirmuel.design/](https://altair.sirmuel.design/)

A fallback is always: [https://github.com/prisma/graphql-playground](https://github.com/prisma/graphql-playground)

It can define custom subscription endpoint \(unlike graphiql\). If used inside Chrome as extension it can use custom proxy plugins. On the other hand, copying large payloads from it is sometimes buggy, and impossible to switch off beautification. Setting variables requires extra clicks + extra windows.
{% endtab %}

{% tab title="Insomnia" %}
I have been using Insomnia \([https://insomnia.rest/graphql/](https://insomnia.rest/graphql/)\) it gives a similar pattern as postman, but with GraphQL support. One thing to note that it does more than just GraphQL, and it is setup as a POST request with the body type as GraphQL.

Some nice features:

* Collections/Folders to organize specific requests in
* Be able to see a complete breakdown of the response, and control any part of the request.
* Be able to set Environments and have specific variables in each, so you can setup a single request and run it against multiple different clusters.
* Multi-Platform
{% endtab %}
{% endtabs %}



