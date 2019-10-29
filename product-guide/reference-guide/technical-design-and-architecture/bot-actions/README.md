# Bot Actions

Maana Knowledge Services form a network of GraphQL endpoints, exposing their types, queries, and mutations for direct access, as well as publishing and subscribing to network events. The Maana Q platform manages these services, providing authentication, reliable messaging, \(automatic\) graph persistence \(with search and querying\), scaling, monitoring, and a rich UX.

Knowledge Services can become Knowledge "Bots" by offering and using "bot actions," which allows the service to interact more directly with you. You can configure, start, stop, and schedule bot actions. Services can report on status and progress for potentially **long-running**, **asynchronous operations**, as well as report any errors or messages.

There are two primary scenarios: 

* Event handling
* Direct query or mutation

### Event Handling

When a Knowledge Service subscribes to and handles an event, such as "fileAdded," it can \(optionally\) create an instance of a BotAction Kind by mutating the CKG. As the service performs its operation, it can periodically update the progress \(if it is deterministic\) and update the status and report errors.

### Queries and Mutations

You can invoke a query or mutation either explicitly \(e.g. train a classifier on labeled data\) or implicitly \(e.g. as part of query graph\). In such cases, the service exposes such queries and mutations as returning a BotAction, which indicates to the UI that these are available.

### Asynchronous Results

One of the primary use cases for BotActions is to support potentially long-running, asynchronous operations. The underlying GraphQL model for queries and mutations is synchronous. For example, the operation:

```python
search(term: String!): [Document!]!
```

can be queried as:

```python
const SEARCH_QUERY = gql`query search($term: String!) {
  search(term: $term) {
    id
    name
    ...
  }
}`
 
 
...
 
 
const documents = await client.query({
  query: SEARCH_QUERY,
  variables: {term: "Kratos"}
})
```

It is thus expected that the set of documents found by the search operation will be returned as part of a single call, despite it being _Invoked_ asynchronously.

This is fine for short-lived operations \(e.g. &lt; 1 minute\), but, in practice, some queries \(or mutations\) can take several minutes, hours, or even days \(e.g. complex Spark or TensorFlow jobs\). In such cases, we'd like a [future-like](https://en.wikipedia.org/wiki/Futures_and_promises) mechanism in which we are given some sort of _token_ that can be used to coordinate access to progress and results. To accomplish this, we propose the following pattern:

```python
searchAction(term: String!, resultKey: String!): BotAction!
searchResult(resultKey: String!): [Document!]!
```

In this case, the original operation has been extended to accept an additional argument, resultKey, which is used to retrieve the results for a particular invocation. A BotAction instance \(generic\) is returned \(if the operation is initiated successfully\) and can be used to track the progress of the operation \(polling or event-based, errors, etc.\). It also records the resultkey value that was used for convenience.

The service must also provide a separate query that returns the actual results that have been generated asynchronously. \(Paging, skips, etc. can be added here as appropriate, but are not part of the BotAction protocol.\)

## Bots

### Schema <a id="BotActions-Schema"></a>

```python
enum BotActionStatus {
  PENDING # initial
  IN_PROGRESS
  STOPPING # request to stop processing
  STOPPED # paused, if operation can be resumed, otherwise ERROR (cancelled)
  ERROR # stopped with service-defined or system-defined error(s)
  COMPLETE # stopped without error
}
 
type BotAction {
  # io.maana.kind
  id: ID!
  name: String!
  # bookkeeping
  created: DateTime!
  lastUpdated: DateTime!
  status: BotActionStatus!
  progress: Float
  errors: [JSON!]
  # operation
  bot: Bot
  kind: Kind
  service: Service!
  eventName: String
  function: Function
  input: InstanceRef
  output: InstanceRef
  # lineage
  parent: BotAction
}
```

### Sample Query <a id="BotActions-SampleQuery"></a>

```python
query botAction($id: ID!) {
  botAction(id: $id) {
    name
    service {
      name
    }
    status
    error
  }
}
```

