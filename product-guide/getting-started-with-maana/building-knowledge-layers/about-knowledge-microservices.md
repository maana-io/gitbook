# About Knowledge Microservices

At this point in solution development, we essentially have a graph database that allows us to interact with the data we have uploaded using GraphQL and a scaffolding of function definitions without the lower level working implementation. 

In this section, we provide an introduction to how microservices can be used to enrich your knowledge graph with computations. We digress from our solution development process to walk through how services fit into the Maana ecosystem. 

Maana provides you with a catalog of pre-created microservices that can significantly bootstrap your solution development. But as your solutions progress, you may need additional, more specific services that need to be created \(typically by developers and/or data scientists\). 

## What is a Knowledge Microservice?

Microservices are small, autonomous services that work together.

In a Microservice Architecture \(such as Maana Q's\) the typical traits shared by microservices are:

* Small in size 
* Messaging enabled
* Bounded by contexts
* Independently deployable
* Decentralized

## Different types of services in the Maana platform

Services in the Maana platform can be split into three types:

* Authored services
  * 
* Wrapped services
  * 
* Workspace as a service
  * 



![](../../../.gitbook/assets/image%20%2815%29.png)

## Service Interactions  <a id="interactions"></a>

* Services can be directly invoked as a standard GraphQL endpoint:
  * from Maana Knowledge Portal, GraphQL, CLI, Python, JavaScript, etc.
  * It's just an HTTP server supporting the GraphQL protocol.
* Services can serve authorized clients:
  * e.g. the Text Classifier is asked to train a new model.
  * e.g. Constraint satisfaction is asked to solve a linear programming problem.
* Services can consume other services as a client:
  * e.g. the Maana Entity Extractor service relies on the Stanford CoreNLP service.
  * e.g. the Shipping Logistics service relies on the Constraint Satisfaction service.
  * e.g. the Text Classifier service needs a collection of text instances.
* Services can publish and subscribe to events:
  * e.g. FileAdded, HasClassification, BotAction

