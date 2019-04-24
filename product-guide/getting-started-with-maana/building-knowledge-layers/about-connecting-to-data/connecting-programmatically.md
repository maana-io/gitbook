# Connecting Programmatically

### Adding data via the CLI

You can upload CSV and JSON files to various GraphQL-based storage targets, e.g., [neo4j-graphql](https://github.com/neo4j-graphql), [Prisma](https://github.com/prismagraphql/prisma) \([OpenCRUD](https://www.opencrud.org/)\), or Maana's KindDB.

The only required argument is `fileOrDir`. Filename are then assumed to match their corresponding GraphQL type definition. For example, `type Person {}` would have data in a file `Person.json` or `Person.csv`. This is especially useful for uploading an entire set of data \(many kinds\) from an entire directory to a **persistent subgraph**.

Otherwise, if uploading a single or multiple files of the same kind but with different names from the corresponding GraphQL type, then the type may be explicitly specified \(`-t`\) and/or the mutation to use \(`-m`\).

{% hint style="info" %}
For more information and examples visit the [Maana CLI github page](https://github.com/maana-io/q-cli) 
{% endhint %}

