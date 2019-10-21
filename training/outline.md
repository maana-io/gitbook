# Outline

## Q Training Experience at a Glance

![Maana Q Training at a Glance](../.gitbook/assets/image%20%2891%29.png)

## Detailed Training Agenda

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Lesson Name</b>
      </th>
      <th style="text-align:left"><b>Goal</b>
      </th>
      <th style="text-align:left"><b>Material Covered</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><a href="basics/basic-orientation/">Orientation</a>
      </td>
      <td style="text-align:left">
        <p>Basic product orientation</p>
        <p></p>
        <p><em>This lesson will teach you Maana terminology and how to navigate through the software</em>
        </p>
      </td>
      <td style="text-align:left">Basic operation of Q - Logging in, creating a workspace</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="basics/hello-world.md">Hello, World</a>!</td>
      <td style="text-align:left">
        <p>Create a microservice with one implemented function</p>
        <p></p>
        <p><em>This lesson is a hands-on exercise to familiarize you with Maana core terminology</em>
        </p>
      </td>
      <td style="text-align:left">&#x2022; What is a workspace? &#x2022; Creating/renaming function &#x2022;
        Adding function field &#x2022; Importing a service to a workspace</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="basics/using-kinds-and-function-to-build-a-knowledge-graph.md">Computational Knowledge Graph</a>
      </td>
      <td style="text-align:left">
        <p>Create a function composition using kinds</p>
        <p></p>
        <p><em>With a hands on exercise, we demonstrate the computation knowledge graph, a technology which sets Maana apart</em>
        </p>
      </td>
      <td style="text-align:left">Introduction to kinds Functional programming 101 &#x2022; inputs and outputs
        &#x2022; side effects and pure functions &#x2022; Compositionality</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="basics/working-with-lists.md">Working with Lists</a>
      </td>
      <td style="text-align:left"><em>It is very often that we have to perform a certain operation on multiple items. To simplify the process of parallel computing, Maana Q allows you to execute functions on multiple items while efficiently caching the result. Maana Q runs the function in parallel using all the available computation resource</em>
      </td>
      <td style="text-align:left">&#x2022; Introduction to the concept of &quot;map&quot; in functional
        programming &#x2022; Automatic caching &#x2022; Limitation of mapping &#x2022;
        Zipping</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="basics/microservices-examples/nlp.md">NLP Example</a>
      </td>
      <td style="text-align:left">
        <p>Learn how to compose functions from multiple microservices. We&apos;ll
          build a model that will extract key entities from a textual source.</p>
        <p></p>
        <p><em>This lesson will recap everything learned so far</em>
        </p>
      </td>
      <td style="text-align:left">Using helper utility functions like word counting</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="basics/microservices-examples/audio-translation.md">Audio translation</a>
      </td>
      <td style="text-align:left">Audio transcription and translation (using maana-media, maana-audio, example
        for using Azure services like maana-azure-speech-to-text, maana-azure-translation)</td>
      <td
      style="text-align:left">Audio transcription and translation (using maana-media, maana-audio, example
        for using Azure services like maana-azure-speech-to-text, maana-azure-translation)</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="methodology/use-case-selection.md">Use Case Selection</a>
      </td>
      <td style="text-align:left">TBD</td>
      <td style="text-align:left">TBD</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="methodology/problem-questions-and-decomposition.md">Top down approach</a>
      </td>
      <td style="text-align:left">Articulate the key element of Maana&apos;s methodology, i.e., Top Down
        Problem Decomposition</td>
      <td style="text-align:left">&#x2022; Problem decompositionTop down thinking</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="methodology/collaboration.md">Collaboration</a>
      </td>
      <td style="text-align:left"><em>Learn how team members might collaborate when building a solution on Q.</em>
      </td>
      <td style="text-align:left">&#x2022; Team collaboration &#x2022; Using workspaces to break down areas
        of development &#x2022; The role of the Knowledge Architect &#x2022; Function
        interfaces as contracts</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="methodology/kickoff-session.md">Project Execution</a>
      </td>
      <td style="text-align:left">TBD</td>
      <td style="text-align:left">TBD</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="advanced/developer-steel-thread.md">Developer Steel Thread</a>
      </td>
      <td style="text-align:left">
        <p>Wrapping existing libraries - Getting started with the Maana CLI (Project
          creation, deployment) and using them in Q</p>
        <p>You&apos;ll learn how to easily onboard existing libraries and code to
          your Q projects</p>
      </td>
      <td style="text-align:left">Maana CLI - mcreate, mdeploy Basic Kubernetes concepts Development pattern
        for creating GraphQL wrapping services for existing libraries</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="advanced/design-patterns.md">Design Patterns</a>
      </td>
      <td style="text-align:left">Learn how to recognize and capture common patterns, such as concept specialization,
        enumeration</td>
      <td style="text-align:left">&#x2022; Reuse &#x2022; Naming convention &#x2022; Combining concepts
        Encapsulation &#x2022; Specialization &#x2022; Modeling inheritance</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="advanced/constraint-satisfaction.md">Constraint satisfaction</a>
      </td>
      <td style="text-align:left">Build a constraint satisfaction model</td>
      <td style="text-align:left">&#x2022; Using templates &#x2022; High order patterns</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="advanced/learning.md">Learning</a>
      </td>
      <td style="text-align:left">This lesson teaches you how to apply an ORDL model as a team (together
        with SMEs, BAs, knowledge architects, developers, testers) to create a
        solution that improves over time</td>
      <td style="text-align:left">&#x2022; What is ORDL? &#x2022; What are examples of observation, reasoning,
        decision and learning functions?</td>
    </tr>
  </tbody>
</table>