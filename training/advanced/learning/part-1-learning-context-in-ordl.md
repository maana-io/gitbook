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

![Piping Consolidation  Knowledge Model Architecture](../../../.gitbook/assets/image%20%2849%29.png)

### Now, looking at this Knowledge Model in Maana... 

These following steps will help illustrate how a Learning component is incorporated in a Knowledge Application. 

**Step 1:** Open the Piping Consolidation Workspace and familiarize with the problem decomposition and Domain Model. 

Workspace found at:

[https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c](https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c)

**Step 2:** Compare the model architecture in the Figure above, with that in the Knowledge Model. Does it follow the same structure?

**Step 3:** Now concentrate on the Function: **RemoveRedundantClasses** \(one level down from the Top PQ\). This function is further decomposed on sequential steps which Generate Pairs of Piping Classes \(generateClassesPairs\), calculates Similarity \(calculateSimilarity\) and remove highly similar classes \(removeHighlySimilarClasses\). See figures below to get an understanding of this decomposition.  

![removeRedundantClasses inside of consolidateClassesinOperatingAsset](../../../.gitbook/assets/image%20%2834%29.png)

![removeRedundantClasses Decomposition](../../../.gitbook/assets/image%20%289%29.png)



