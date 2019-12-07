---
description: Basic Learning technique explained through and example
---

# Passive Learning

### **Introduction**

Part 2 illustrates a Data Science 'Learning' technique which can be applied in different Knowledge Applications. Note that this example does not require prior knowledge in Data Science. 

In this example, Gordon Banks is the owner of a chain of restaurants. He is interested in knowing how people feel about his restaurants. While he has done surveys and receives ratings through different channels, he is interested in creating a predictive model, which can help him understand the true sentiment of customers behind online comments. Gordon recruited Ana Lewis, a Data Scientist who has now prior experience in the restaurant business.

### Training a Model

Ana started by compiling an initial dataset of customer reviews over Yelp. She divided this set into 2 piles randomly, which she called Training Dataset and Test Dataset \(which she put away and saved for later\). Further, she divided the Training Dataset in 2 groups. **Group 1: Positive comments** -  reviews with 4 stars or more. **Group 2: Negative comments** -  reviews with 3 stars or less. She went over this dataset with Gordon, verifying the veracity of the comments and her initial classification.

Ana then went to Maana Q, and created a 'Training Function' which generates a predictive model Gordon can use to uncover the sentiment under a customer written comment. You can run this function by opening the workspace below, selecting **train,** and running it via the Maana Q User Interface \(see screenshot with output below\). 

[https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8](https://cstrainingstable.knowledge.maana.io/workspace/96538995-2611-47b6-a650-51a9c66233d8)

![](../../../.gitbook/assets/image%20%2898%29.png)

While Gordon is not necessarily interested in this particular function, Ana tells him, a Logistic Regression model is the most appropriate Machine Learning approach given the dataset she looked at.  She also mentions that the performance or accuracy of this model is at 65% which is not great, but better than random guessing. Gordon is not thrilled, and asks Ana if he can see some predictions.

### Evaluating the Accuracy of Predictions

Ana told Gordon, the next step is to run her Machine Learning model with the Test Dataset, which was not used for training. For that, she created the **evaluate** function which she ran to show the results to Gordon. Most of the results looked as expected \(image below\), but the Test Dataset was fairly small, so Gordon was not convinced this model could work accurately for a large number of comments. 

![](../../../.gitbook/assets/image%20%28146%29.png)

### Predicting the Sentiment of a New Comment

After that, Ana suggested to Gordon to type a comment on his own \(free text\) and see what the model would predict. For that, she referred him to the **predictOne** function. Gordon typed on the Maana Q UI a random comment he thought of, clicked Run and then saw the output in the Function Results panel \(image below\). He tried a few more comment, and thought that in some cases the predicted sentiment was not accurate. He asked Ana how he could help improve the accuracy of the model, given that he has no background in Data Science, nor a desire to switch careers...

![](../../../.gitbook/assets/image%20%2855%29.png)

### Feedback to the Model

Ana created another function called **feedback**. Here, she asked Gordon to enter labeled data, i.e., customer comments along with their appropriate sentiment \(either negative or positive\). She told him this would help the model improve with time. One of Gordon entries is shown below.

![](../../../.gitbook/assets/image%20%2863%29.png)

Ana mentioned that these new entries from Gordon will now be part of the Training Dataset used in the function **train**. She then proceeded to run that function giving a model\_id of 4 \(equivalent to model version number\). 

After that, she asked Gordon to come back to the **predictOne** function, and enter one of the same comments he used in his feedback.  After doing that, Gordon noticed that the predicted sentiment was 'Positive', which is consistent with his feedback and different than the initial prediction \(see Predicting the Sentiment of a New Comment above\), which was inaccurately predicted as Negative.  

![](../../../.gitbook/assets/image%20%288%29.png)

Through these steps, Gordon gained an understanding of how he can evaluate the accuracy of the model Ana created for him, and how he can improve its accuracy by providing feedback. Ana went to summarize the feedback loop mechanism in the figure below. 

![](../../../.gitbook/assets/image%20%28132%29.png)

Can you think of any limitations of this Feedback Loop architecture?



