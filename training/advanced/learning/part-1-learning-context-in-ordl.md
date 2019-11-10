---
description: Piping Consolidation Example
---

# Part 1 - Learning as part of ORDL

### Introduction

Piping is a key component of essentially every facility in oil & gas, Across the value chain, piping is a common asset which represents a significant portion of the Capital Expenditures in any given development project. In Operations, piping is also critical to operating expenses, reliable operations and operating expenses, to mention a few areas. 

Most oil & gas operators maintain a catalog of Piping Classes \(_each class corresponding to one type of Piping, with specifications on operating pressures, temperatures, corrosion allowance, service, etc_.\). Proliferation of Piping Classes is a common problem in the industry, which has connection with sub-optimal capital allocation, increased procurement and warehousing costs and increased operational risks. 

It is also common for Piping Subject Matter Experts to spend significant effort in manually consolidating piping classes across business units. The process can sometimes be subjective as well. This example corresponds to a Knowledge Application which is intended to support the work of Piping SMEs as they perform consolidation. 

### Applying ORDL

**Observe:** A Central Engineering Department in an oil & gas operator is responsible for creating a standard catalog of piping classes , for all Major Capital Projects \(MCPs\) and Operating Assets to use. Often times, Business Units create new classes leading to unnecessary proliferation. 



business unit class specifications, which range in the dozens per each equipment class, like pipe class specifications**.**

**Reason** According to Piping SMEs the process of consolidation can be decomposed into rules, i.e., piping with the same service, same corrosion allowance and same specifications can be considered as equivalent. 

**Decide:** Ultimate decision on consolidation are to be made by SMEs.  

**Learn** The process of consolidation can be explained in rules, but in reality a large part of the SME knowledge cannot be easily encoded.

### Knowledge Model Architecture

The diagram below shows a representation of the architecture of a Knowledge Model of Piping Consolidation. 

![Piping Consolidation  Knowledge Model Architecture](../../../.gitbook/assets/image%20%2849%29.png)

### Now, looking at this Knowledge Model in Maana... 

**Step 1:** Open the Piping Consolidation Workspace and familiarize with the problem decomposition and Domain Model. 

[https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c](https://cstrainingstable.knowledge.maana.io/workspace/a2637150-eb0a-4f85-aca9-00ca7e018b1c)

**Step 2:** Compare the model architecture in the Figure above, with that in the Knowledge Model. 

**Step 3:** Now concentrate on the Function: **RemoveRedundantClasses**

![removeRedundantClasses inside of consolidateClassesinOperatingAsset](../../../.gitbook/assets/image%20%2834%29.png)

![removeRedundantClasses Decomposition](../../../.gitbook/assets/image%20%289%29.png)

