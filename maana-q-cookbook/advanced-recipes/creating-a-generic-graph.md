# Creating a Generic Graph

## About this Tutorial <a id="about-this-tutorial"></a>

This Knowledge Service provides the concept of a generic graph \(e.g. nodes and edges\) using three distinct microservices:

* **Model Service**: Prisma-based GraphQL persistence of the Maana Graph domain model.
* **Logic Service**: graphql-yoga-based service that provides domain-specific logic.
* **UI Service**: React-based application \(assistant\) that provides a custom interface for managing and manipulating Graphs.

## 1. Assembling the Service <a id="1-assembling-the-service"></a>

This section describes how this service was assembled such that it could be recreated or used as an example of how other services might be built.

### Prerequisites <a id="prerequisites"></a>

For convenience, the following commands should be installed globally:

```text
npm i -g create-react-app prisma graphql-yoga lerna graphql-cli graphql-cli-maana
```

#### maana-graph: Lerna monorepo <a id="maana-graph-lerna-monorepo"></a>

1. Create a root directory to contain the project tree:

```text
mkdir maana-graph
cd maana-graph
```

2. Unify the build of the three servies using [Lerna](https://github.com/maana-io/q-tutorials/blob/master/maana-graph):

```text
lerna init
```

3. Lerna requires that the subprojects reside in a specific location:

```text
mkdir packages
```

#### maana-graph-model: Model service using Prisma <a id="maana-graph-model-model-service-using-prisma"></a>

```text
cd packages
prisma init maana-graph-model
# select 'Create new database'
# select 'MySQL'
cd maana-graph-model
```

### **Update the network ports** <a id="update-the-network-ports"></a>

Edit the `prisma.yml` and `docker-compose.yml` files to change the network ports, as appropriate.

### **Create the data model** <a id="create-the-data-model"></a>

1. Create a folder to hold all the models for the domain, which will be merged together:

```text
mkdir models
```

2. Create and edit `models/graph.gql` to hold the domain model:

```text
enum VertexType {
  Empty
  Special
}

enum VertexSubtype {
  SpecialChild
}

enum EdgeType {
  EmptyEdge
  SpecialEdge
}

# A collection of vertices and edges between them
type Graph {
  # Unique identity of graph instance
  id: ID! @unique
  name: String
  vertices: [Vertex!]! @relation(name: "GraphVertices")
  edges: [Edge!]! @relation(name: "GraphEdges")
}

# Node of a graph
type Vertex {
  # Unique identity of vertex instance
  id: ID! @unique

  # Horizontal position on the diagram
  x: Float!

  # Vertical position on the diagram
  y: Float!

  # Edges where this vertex is the target (i.e., inbound)
  edgesTarget: [Edge!]! @relation(name: "VertexEdgesTarget")

  # Edges where this vertex is the source (i.e., outbound)
  edgesSource: [Edge!]! @relation(name: "VertexEdgesSource")

  # Display label
  title: String

  # Node shape and behavior
  type: VertexType

  subtype: VertexSubtype
}

# Edge connecting two vertices in a graph
type Edge {
  # Unique identity of edge instance
  id: ID! @unique
  source: Vertex! @relation(name: "VertexEdgesSource")
  target: Vertex! @relation(name: "VertexEdgesTarget")
  # visual elements
  title: String
  type: EdgeType
}
```

### **Test Data** <a id="test-data"></a>

1. Create a `data` folder to hold both _raw_ source data and converted _NDF_ data:

```text
mkdir -p data/raw
```

2. Add the following test data to `data/raw/Graph.json`:

```text
[
  {
    "id": "test-g00",
    "name": "Test Graph #00",
    "vertices": ["test-v00", "test-v01", "test-v02", "test-v03"],
    "edges": ["test-e00", "test-e01"]
  }
]
```

and `data/raw/Vertex.json`:

```text
[
  {
    "id": "test-v00",
    "title": "Node A",
    "x": 258.3976135253906,
    "y": 331.9783248901367,
    "type": "Special"
  },
  {
    "id": "test-v01",
    "title": "Node B",
    "x": 593.9393920898438,
    "y": 260.6060791015625,
    "type": "Empty",
    "subtype": "SpecialChild"
  },
  {
    "id": "test-v02",
    "title": "Node C",
    "x": 237.5757598876953,
    "y": 61.81818389892578,
    "type": "Empty"
  },
  {
    "id": "test-v03",
    "title": "Node C",
    "x": 600.5757598876953,
    "y": 600.81818389892578,
    "type": "Empty"
  }
]
```

and, lastly, `data/raw/Edge.json`:

```text
[
  {
    "id": "test-e00",
    "source": "test-v00",
    "target": "test-v01",
    "type": "SpecialEdge"
  },
  {
    "id": "test-e01",
    "source": "test-v02",
    "target": "test-v03",
    "type": "EmptyEdge"
  }
]
```

## **2. Build the Docker Container** <a id="2-build-the-docker-container"></a>

This service requires the docker container be started, the data models be merged corresponding tables created in the database, and seed data converted and imported. 1. Use NPM to help manage these actions:

```text
npm init -y
npm i -D babel-cli gql-merge npm-run-all
```

2. And add the following scripts:

```text
"scripts": {
    "merge": "gql-merge models/**/*.gql > datamodel.graphql",
    "convert": "gql mload data/raw -n data/ndf -p model",
    "docker-up": "docker-compose up -d",
    "deploy": "prisma deploy --force && gql get-schema -p model",
    "reset": "prisma reset --force && rm -rf data/ndf",
    "import": "prisma import --data data/ndf",
    "prepublish": "npm-run-all merge reset convert docker-up deploy import"
  },
```

### 1. maana-graph-logic: Logic service using graphql-yoga <a id="1-maana-graph-logic-logic-service-using-graphql-yoga"></a>

Now implement a \(GraphQL-based\) logic layer that uses the domain model \(GraphQL persistence layer\) per [Prisma's guidance](https://www.prisma.io/docs/tutorials/build-graphql-servers/development/build-a-graphql-server-with-prisma-ohdaiyoo6c). You could just expose the model service directly, but this has a number of [disadvantages](https://www.prisma.io/docs/tutorials/build-graphql-servers/development/build-a-graphql-server-with-prisma-ohdaiyoo6c#why-not-use-the-prisma-api-directly-from-your-client-applications).

```text
mkdir -p packages/maana-graph-logic/src
cd packages/maana-graph-logic
npm init -y
npm add graphql-yoga prisma-binding
npm add -D npm-run-all
```

### **2. Setup the GraphQL config** <a id="2-setup-the-graphql-config"></a>

Let's configure two different GraphQL projects \(endpoints\): our model service and our logic service. These should be configured in `.graphconfig.yml`:

```text
projects:
  model:
    schemaPath: src/generated/prisma.graphql
    extensions:
      endpoints:
        default: 'http://localhost:4468'
  app:
    schemaPath: src/schema.graphql
    extensions:
      endpoints:
        default: 'http://localhost:8068'
```

### **3. Get the generator model schema** <a id="3-get-the-generator-model-schema"></a>

Anytime the the model schema changes \(and is redeployed\), you'll need to update your local copy:

```text
gql get-schema -p model
```

### **4. Edit the logic service schema** <a id="4-edit-the-logic-service-schema"></a>

Instead of surfacing all the raw database operations directly, provide an abstraction layer that supported the needs of our application.

Edit `src/schema.graphql` so that it has the following "business logic":

```text
# import VertexType, VertexSubtype, EdgeType from "./generated/prisma.graphql"
# import Graph, Vertex, Edge from "./generated/prisma.graphql"

type Query {
  graphs: [Graph!]!
  graph(id: ID!): Graph
  vertex(id: ID!): Vertex
  edge(id: ID!): Edge
}

type Mutation {
  # Create a graph with an optional name
  createGraph(name: String): Graph

  # Create a vertex in a graph
  createVertex(
    graphId: ID!
    name: String
    x: Float
    y: Float
    type: VertexType
    substyle: VertexSubtype
  ): Vertex

  # Create an edge between two vertices in a graph
  createEdge(
    graphId: ID!
    fromVertex: ID!
    toVertex: ID!
    name: String
    style: EdgeType
  ): Edge
}
```

### **5. Implement the resolvers for the logic** <a id="5-implement-the-resolvers-for-the-logic"></a>

Edit `src/index.js` to create the server and implement the resolvers:

```text
const { GraphQLServer } = require("graphql-yoga");
const { Prisma, forwardTo } = require("prisma-binding");

const PRISMA_ENDPOINT = "http://localhost:4468";
const SERVER_PORT = 8068;

const resolvers = {
  Query: {
    graph: (_, { id }, context, info) =>
      context.prisma.query.graph(
        {
          where: { id }
        },
        info
      ),
    vertex: (_, { id }, context, info) =>
      context.prisma.query.vertex(
        {
          where: { id }
        },
        info
      ),
    edge: (_, { id }, context, info) =>
      context.prisma.query.edge(
        {
          where: { id }
        },
        info
      )
  },
  Mutation: {
    createGraph: (_, { name }, context, info) =>
      context.prisma.mutation.createGraph({ data: { name } }, info),
    createVertex: (
      _,
      { name, x = 0.0, y = 0.0, style, substyle, graphId },
      context,
      info
    ) =>
      context.prisma.mutation.createVertex(
        {
          data: {
            name,
            x,
            y,
            style,
            substyle,
            graph: { connect: { id: graphId } }
          }
        },
        info
      ),
    createEdge: (
      _,
      { graphId, name, fromVertex, toVertex, style },
      context,
      info
    ) =>
      context.prisma.mutation.createEdge(
        {
          data: {
            name,
            style,
            graph: { connect: { id: graphId } },
            fromVertex: { connect: { id: fromVertex } },
            toVertex: { connect: { id: toVertex } }
          }
        },
        info
      )
  }
};

const server = new GraphQLServer({
  typeDefs: "src/schema.graphql",
  resolvers,
  context: req => ({
    ...req,
    prisma: new Prisma({
      typeDefs: "src/generated/prisma.graphql",
      endpoint: PRISMA_ENDPOINT
    })
  })
});

const options = {
  port: SERVER_PORT
};

server.start(options, () =>
  console.log(
    `GraphQL server is running on http://localhost:${options.port || 4000}`
  )
);
```

### **6. Sample Graph** <a id="6-sample-graph"></a>

```text
mutation createGraph {
  createGraph(name: "Graph #00") {
    id
  }
}

mutation createVertices {
  v00: createVertex(graphId: "cjjq5lfty002r0b73kuq62jp4", name: "A") {
    id
  }

  v01: createVertex(graphId: "cjjq5lfty002r0b73kuq62jp4", name: "B") {
    id
  }
}

mutation createEdges {
  e00: createEdge(
    graphId: "cjjq5lfty002r0b73kuq62jp4"
    name: "f"
    fromVertex: "cjjq5lpgn002v0b73s79pc95c"
    toVertex: "cjjq5lph8002z0b731gclqam0"
  ) {
    id
  }
}

query queryGraph {
  g: graph(id: "cjjq5lfty002r0b73kuq62jp4") {
    name
    edges {
      id
      name
      style
      fromVertex {
        id
        name
        x
        y
        style
        substyle
      }
      toVertex {
        id
        name
        x
        y
        style
        substyle
      }
    }
  }
}
```

### 7. UI service using create-react-app <a id="7-ui-service-using-create-react-app"></a>

A custom user interface has been provided that allows for the creation and editing of a graph in a domain-specific way.

This is implemented as a small React app built around the [react-digraph](https://github.com/uber/react-digraph) component.

```text
cd packages
create-react-app maana-graph-assist
cd maana-graph-assist
npm i apollo-boost react-apollo graphql graphql-tag
```

### **8. Create a GraphQL client to logic service** <a id="8-create-a-graphql-client-to-logic-service"></a>

Edit \`src/index.js' to reflect the following changes:

```text
import React from "react";
import ReactDOM from "react-dom";
import { ApolloProvider } from "react-apollo";
import ApolloClient from "apollo-boost";
import gql from "graphql-tag";
//
import "./index.css";
import App from "./App";
import registerServiceWorker from "./registerServiceWorker";

const LOGIC_ENDPOINT = "http://localhost:8068";
```

The main application, `src/App.js`, renders the user interface and communicates via GraphQL to the logic service:

```text
import React, { Component } from "react";
import { ApolloConsumer, Query, Mutation } from "react-apollo";
import ApolloClient from "apollo-boost";
import gql from "graphql-tag";
//
import logo from "./logo.svg";
import "./App.css";
import Graph from "./Graph";
```

