---
description: Basic Learning technique explained through and example
---

# Part 2 - Passive Learning

### **Introduction**

Part 2 illustrates a Data Science 'Learning' technique which can be applied in different Knowledge Applications. Note that this example does not require prior knowledge in Data Science. 

In this example, Gordon Banks is the owner of a chain of restaurants. He is interested in knowing how people feel about his restaurants. While he has done surveys and receives ratings through different channels, he is interested in creating a predictive model, which can help him understand the true sentiment of customers behind online comments. Gordon recruited Ana Lewis, a Data Scientist who has now prior experience in the restaurant business.

### Training a Model

Ana started by compiling an initial dataset of customer reviews over Yelp. She divided this set into 2 piles randomly, which she called Training Dataset and Test Dataset \(which she put away and saved for later\). Further, she divided the Training Dataset in 2 groups. **Group 1: Positive comments** -  reviews with 4 stars or more. **Group 2: Negative comments** -  reviews with 3 stars or less. She went over this dataset with Gordon, verifying the veracity of the comments and her initial classification.

Ana then went to Maana Q, and created a 'Training Function' which generates a predictive model Gordon can use to uncover the sentiment under a customer written comment. You can run this function by opening the workspace below, selecting **train,** and running it via the Maana Q User Interface \(see screenshot with output below\). 

[https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8](https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8)

![](../../../.gitbook/assets/image%20%2886%29.png)

While Gordon is not necessarily interested in this particular function, Ana tells him, a Logistic Regression model is the most appropriate Machine Learning approach given the dataset she looked at.  She also mentions that the performance or accuracy of this model is at 65% which is not great, but better than random guessing. Gordon is not thrilled, and asks Ana if he can see some predictions.

### Evaluating the Accuracy of Predictions

Ana told Gordon, the next step is to run her Machine Learning model with the Test Dataset, which was not used for training. For that, she created the **evaluate** function which she ran to show the results to Gordon. Most of the results looked as expected \(image below\), but the Test Dataset was fairly small, so Gordon was not convinced this model could work accurately for a large number of comments. 

![](../../../.gitbook/assets/image%20%28127%29.png)

### Predicting the Sentiment of a New Comment

After that, Ana suggested to Gordon to type a comment on his own \(free text\) and see what the model would predict. For that, she referred him to the **predictOne** function. Gordon typed on the Maana Q UI a random comment he thought of, clicked Run and then saw the output in the Function Results panel \(image below\). He tried a few more comment, and thought that in some cases the predicted sentiment was not accurate. He 

![](../../../.gitbook/assets/image%20%2866%29.png)

4th Feedback the Model -&gt; This connects back to the training set. 

Training goals:

1. Show how SME feedback loop works:

1. Prepare labeled data, unlabeled data, and test data. 
2. Train a model.
3. Evaluate the model on test data. Figure out mistakes the model made. 
4. SMEs give feedback to the model \(teacher to student approach\) 
5. Retrain the model. 
6. Reevaluate the model to see how SME feedback helps.
7. The loop continues.

      The point here is to show that SME feedback can improve model quality.

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



