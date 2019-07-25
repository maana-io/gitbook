# Building The Knowledge Layer

The Solution Lifecycle is the process that walks you through deconstructing the high level problem-question you're trying to answer, then building out the domain/function modeling that will enable you to create a solution graph. With your solution graph, you'll then move on to connecting to your data. Next, you'll build out or import relevant knowledge services and finally build a knowledge app.

The image below is a high-level map to visualize the entire Solution Lifecycle. This map is referenced throughout this documentation as a go-by so you know where you are in the process.

![Diagram of the Solution Lifecycle](https://maanaimages.blob.core.windows.net/maana-q-documentation/k1.png)

### 1. Problem Decomposition <a id="1-problem-decomposition"></a>

Problem decomposition allows us to move from a general business objective to user requirements. To define the problem domain, Maana works recursively through a problem decomposition process. Taking the business objective and breaking it down to determine the required concepts, queries and mutations needed.

![Problem Decomposition](https://maanaimages.blob.core.windows.net/maana-q-documentation/k2.png)

Learn more about problem-questions and the decomposition process here:

{% page-ref page="what-are-problem-questions.md" %}

### 2. Domain and Function Modeling <a id="2-domain-and-function-modeling"></a>

In this step, you'll assemble the concepts and functions into a solution graph.

![Domain &amp; Function Modeling](https://maanaimages.blob.core.windows.net/maana-q-documentation/k3.png)

Learn more about domain and functional modeling here:

{% page-ref page="domain-and-function-modeling.md" %}

### 3. Connect to Data <a id="3-connect-to-data"></a>

Here, you'll implement the computational layer that solves the original business objective.

![Connecting to Data](https://maanaimages.blob.core.windows.net/maana-q-documentation/k4.png)

Learn more about how to hydrate your models from various data sources here:

{% page-ref page="about-connecting-to-data/" %}

### 4. Build or Import the Relevant Knowledge Microservices <a id="4-build-the-knowledge-microservices"></a>

The Maana SDK offers several service templates for popular languages to aid developers and data scientists in the task of creating and deploying Maana-ready microservices that can then be easily added to the platform via URL as reusable building blocks of the solution. 

![Build the Knowledge Microservices and the accompanying App, then Deploy the App](https://maanaimages.blob.core.windows.net/maana-q-documentation/k5.png)

Learn more about how to build, deploy and import Knowledge Microservices here:

{% page-ref page="about-knowledge-microservices.md" %}

### 5. Build and Deploy the Knowledge Application

To wrap up the process, a front-end application is created over the CKG for end-users.

Learn more about how to build, deploy and import Knowledge Applications here:

{% page-ref page="../creating-knowledge-applications.md" %}

