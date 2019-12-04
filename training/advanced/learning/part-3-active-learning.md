---
description: Advanced Learning technique explained through and example
---

# Active Learning

### **Introduction**

One of the limitations of the Passive Learning technique shown in [Part 2 ](part-2-passive-learning.md)is the effort the SME \(the restaurant owner in Part 2 example\) needs to spend in labeling data used to further train the prediction model. Active learning on the contrary, looks at minimizing the effort on labeling data so that SME's involvement is routed to areas in which the model needs it the most. 

### **How it Works**

Refer to the same workspace as Part 2: 

[https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8](https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8)

On the Main Functions Knowledge Graph, look at the 2 functions: **askSmartQuestions** and **answerSmartQuestions**. 

![](../../../.gitbook/assets/image%20%2876%29.png)

In this architecture, the model predicts not only sentiments \(negative or positive given a written comment\), nut also provides an indication of its prediction confidence. This parameter is often related to how close the new observation is to the training set. If the confidence is low, the model will pass the comment to the **askSmartQuestions** function. This function will in turn pass the comment in form of a question to the SME, so that he/she can validate or correct the prediction. 



