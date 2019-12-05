---
description: Piping Consolidation Example
---

# Part 1 - Learning as part of ORDL

### Introduction

Piping is a key component of essentially every facility in oil & gas, Across the value chain, piping is a common asset which represents a significant portion of the Capital Expenditures in any given development project. In Operations, piping is also critical to operating expenses, reliable operations and operating expenses, to mention a few areas. 

Most oil & gas operators maintain a catalog of Piping Classes \(_each class corresponding to one type of Piping, with specifications on operating pressures, temperatures, corrosion allowance, service, etc_.\). Proliferation of Piping Classes is a common problem in the industry, which has connection with sub-optimal capital allocation, increased procurement and warehousing costs and increased operational risks. 

It is also common for Piping Subject Matter Experts to spend significant effort in manually consolidating piping classes across business units. The process can sometimes be subjective as well. This example corresponds to a Knowledge Application which is intended to support the work of Piping SMEs as they perform consolidation. 

### Applying ORDL

**Observe:** A Central Engineering Department in an oil & gas operator is responsible for creating a standard catalog of piping classes , for all Major Capital Projects \(MCPs\) and Operating Assets to use. Often times, Business Units create new classes with unique identifiers \(Piping Class Codes\) which leads to unnecessary proliferation.

**Reason:** Consolidation of Piping Classes could be looked under different lenses. **A first lens**, is of identifying **redundancies**. These are cases where 2 Piping Classes have the exact same specifications, but they are identified under different Piping Class ID. A **second lens**, is associated to **reliability**. SMEs might be interested in substituting unreliable Piping Classes, for the most similar ones which have better reliability. A **third lens** is cost. Piping Classes deemed as **cost inefficient** can also be substituted for similar classes which are less costly. 

**Decide:** In this example, a Piping SME is the ultimate responsible for deciding when to consolidate 2 Piping Classes into 1. For that, the Knowledge Application calculates a Similarity Score for a given pair of Piping Classes. This similarity score is based on Business Rules and Machine Learning techniques. 

**Learn:** Like many technical domains, the level of complexity of Piping Consolidation can be quite high. This is partly due to the multitude of factors which are involved, \(_e.g. Material Science, Process Engineering, Mechanical Engineering, Chemical Engineering, Manufacturing_\), and also to the degree of subjectivity and SME-experience which involves. For a Knowledge Application to be effective, it is therefore imperative to 'learn' new rules of consolidation via the interaction of the user with the application. 

### Knowledge Model Architecture

The diagram below shows a representation of the architecture of a Knowledge Model of Piping Consolidation, drawing from the ORDL methodology. 

![Piping Consolidation  Knowledge Model Architecture](../../../.gitbook/assets/image%20%2856%29.png)

### Now, looking at this Knowledge Model in Maana... 

These following steps will help illustrate how a Learning component is incorporated in a Knowledge Application. In this case, Piping SMEs provide feedback to the Knowledge Application. In some cases, where SMEs believe a given pair or pipes should not be consolidated, they would enter that information in a customized User Interface. This information will be routed to the backend, which will be weighed depending on the seniority and level of engagement of the user. 

**Step 1:** Open the Piping Consolidation Workspace and familiarize with the problem decomposition and Domain Model. 

Workspace found at:

[https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c](https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c)

**Step 2:** Compare the model architecture in the Figure above, with that in the Knowledge Model. Does it follow the same structure?

**Step 3:** Now concentrate on the Function: **RemoveRedundantClasses** \(one level down from the Top PQ\). This function is further decomposed on sequential steps which Generate Pairs of Piping Classes \(generateClassesPairs\), calculates Similarity \(calculateSimilarity\) and remove highly similar classes \(removeHighlySimilarClasses\). See figures below to get an understanding of this decomposition.  

![removeRedundantClasses inside of consolidateClassesinOperatingAsset](../../../.gitbook/assets/image%20%2838%29.png)

![removeRedundantClasses Decomposition](../../../.gitbook/assets/image%20%2812%29.png)

**Step 4:** Now, concentrate on the function **calculateSimilarity**. Compare the structure of this function to the Architecture Diagram at the beginning of this section. 

![](../../../.gitbook/assets/image%20%2891%29.png)

**Step 5:** Note that the function **calculateCompoundSimilarity** includes an algorithm to merge the resulting similarity scores of the 3 methods used into one single result. The more feedback a given pair of Piping Classes receives, the more prevalent active learning would be in the compound score. 

**Step 6:** Now, look inside the function **incorporateActiveLearningSimilarity** \(figure below\). This function weighs the Seniority Level of the SME who provides feedback, and his/her Level of Engagement with the application. This is, the more feedback a given user provides, the more weigh his/her opinion would carry. Discuss the benefits and drawbacks of this feedback architecture.  

![](../../../.gitbook/assets/image%20%2835%29.png)

Note that this exercise is meant to provide an example of how Learning can be an integral component of a Knowledge Application. The architecture here demonstrated is not the only one, or not even the best approach for all circumstances. For instance, a group of people might consider a consensus-type of feedback, or a hierarchical-one in which an approver is the gate-keeper for transmitting feedback onto the model. These 2 mechanisms could also be represented by different function decomposition architectures. 

For more details on Data Science techniques for Passive and Active Learning, please refer to [Part 2](part-2-passive-learning.md) and [Part 3](part-3-active-learning.md) of this section. 

