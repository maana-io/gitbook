---
description: Advanced Learning technique explained through and example
---

# Part 3 - Active Learning

### **Introduction**

One of the limitations of the Passive Learning technique shown in [Part 2 ](part-2-passive-learning.md)is the effort the SME \(the restaurant owner in Part 2 example\) needs to spend in labeling data used to further train the prediction model. Active learning on the contrary, looks at minimizing the effort on labeling data so that SME's involvement is routed to areas in which the model needs it the most. 

### **How does it work**

Refer to the same workspace as Part 2: 

[https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8](https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8)

On the Main Functions Knowledge Graph, look at the 2 functions: **askSmartQuestions** and **answerSmartQuestions**. 

![](../../../.gitbook/assets/image%20%2875%29.png)

This is, the model predicted labels \(negative or positive sentiments in the restaurant example\), also include an indication of confidence. This parameter is often related for how close the new observation is to the training set. If confidence is low, the model will ask the user for feedback on those observations. If the confidence is high, the model would opt for not asking the SME for feedback. 

What if the model can ask questions to the SME on items where it has low confidence...

Show Function asking SME, this could be configured in a UI

The model trains with limited input from SME.



SME gives complex observations, the model comes back with questions on sentences it has less confidence on... 

PredictAll is a function where the user inputs a new test set and the function returns classification of those entries... datasets with low confidence are passed on to the askSmarkQuestion Function...

answer question is connected to a UI... Speeds up the process of feedback... 



You can show the LabeledSentence Kind





questions back to the user on those cases where confidence is low. 

Text classification, e.g. 

1. Given a piece of text \(e.g. a sentence, a short paragraph\), predict the "class" of the text. 
2. The classes are data dependent. Could be "Positive", "Negative" for customer review data. Could be "High Risk", "Low Risk", "Medium Risk" for risk data. 
3. The use case is populated with 1000 Yelp reviews, with Positive and Negative labels. \(Other datasets, such as IMDB movie review, are available and can be selected\)

2. Show how active learning can improve the model faster, with less effort from SMEs.

1. Prepare labeled data, unlabeled data, and test data. 
2. Train a model.
3. Let the model make prediction on a pool of unlabeled data to evaluate itself. 
4. Let the model ask SMEs for help \(student to teacher approach\)
   * option 1: the model asks random questions from the pool of unlabeled data. 
   * option 2: the model asks "smart" questions \(based on active learning technique\).
5. SMEs answer questions. 
6. Retrain the model. 
7. Reevaluate the model to see how SME feedback helps.

      The point here is to show that asking "smart" questions can improve model quality faster than asking random questions. 

