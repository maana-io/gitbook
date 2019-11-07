# Connect Knowledge Services

### Assumptions:

* A service whether managed or unmanaged has been registered with Maana Q and been made available to the user via the Inventory
* Kinds, Queries and Mutations will be handled in the context panel \(Schema editor etc.\) in the same manner as regular Kinds \(ability to edit Fields, Types, etc.\)
* Have not included the handling of Bots here. Can expand this to include if necessary

### User stories: 

#### **FIND** a Service

* User searches for the desired Service through Workspace search
* Once found, the user can drag onto the Knowledge Graph \(KG\)/Query Graph \(QG\) canvas the Service as a whole, or specific Kinds/Queries/Mutations
* If specific Kinds/Queries/Mutations have been selected from the search results and dragged onto the canvas, and if this Service was not a part of the WS then that Service and its Kinds/Queries/Mutations should get added to the current Workspace’s Inventory

#### **CONNECT** a Service to components of the KG in a Workspace

The goal here is to add the Service’s capabilities to my KG. For example, given the lat/long data that I have as a part of my Well Kind, I want to bring a Google Maps-like service that provided a lot/long input, returns the name of a location \(city\)

* Once the user has located the desired Service, the next step is to connect the following components of a service to existing Kinds on the KG
  * Kinds
    * The user can preview the Kind schemas on the canvas and click to drag and create connections between relevant Fields between the two schemas
    * The system should only allow connections between matching Field Types
    * If the user attempts to connect mismatched Types, then they should be shown the appropriate error message
    * The status indicator for the Kind should reflect any error states
  * Queries
    * Though similar to the structure of Kinds \(Fields and their Types with In and Out ports\), Queries are different in that they some of the Fields will represent the input\(s\) to the Query and one will represent the Query output
    * The user should be able to clearly identify which Fields are inputs/output
    * In the case of a Query to a Kind connection, the appropriate connection will be one where the compulsory\(!\) input Fields for the Query have been furnished via a connection from a Kind
    * Once a Query has been appropriately connected, its appropriate name and output Kind should be added as a Field to the Kind that furnished the input Query Fields
  * Mutations
    * These will be handled just like Queries

#### **INVOKE** Queries and Mutations

* Certain services can become Bots by offering and using "bot actions," which allows the service to interact more directly to users
* A user can invoke a Query or Mutation either explicitly \(e.g., train a classifier on labeled data\) or implicitly \(i.e., as part of Query Graph\)
* For explicit Queries/Mutations, the user can specify input parameters through the UI, in the KG \(design TBD\)

### Export Workspace Schema to a Knowledge Microservice Implementation

#### Via the UI

From within the Admin Action Panel, select the "Test" button for a workspace as a service.

![Admin Action Panel Test Service Schema Mode](../../.gitbook/assets/image%20%287%29.png)

Copy the definition the service from the GraphQL SDL panel which one can then paste into the micro-service implementation.

#### Via the CLI

1. Design a service in Maana Knowledge Portal Workspace.
2. Implement functions in a code-based microservice.
3. Use the CLI mcreate command to generate a boilerplate Maana Knowledge Microservice in a preferred language.
4. Add the workspace as a project to my graphqlconfig, e.g.:

```text
projects:
  logic:
    schemaPath: schema.graphql
    extensions:
      endpoints:
        default:
          url: 'http://localhost:8053/graphql'
          headers:
            Authorization: 'Bearer ${env:MAANA_AUTH_TOKEN}'
  workspace:
    schemaPath: workspace.schema.graphql
    extensions:
      endpoints:
        default:
          url: >-
https://knowledge.foo.io:8443/service/sdsd8ec6-a75e-4b99-9be7-7y40a65df3g4/graphql
          headers:
            Authorization: 'Bearer ${env:MAANA_AUTH_TOKEN}'
```

After following the standard authentication steps, fetch the workspace schema by issuing the following command:

`gql get-schema -p workspace`

Now, one can easily copy-and-paste the definition the service needs from the resulting workspace.schema.graphql. No need to manually recreate types, queries, mutations, and subscriptions that were already designed using the Maana Workspace UI.

