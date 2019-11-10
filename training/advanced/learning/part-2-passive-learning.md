---
description: Basic Learning technique explained through and example
---

# Part 2 - Passive Learning

### **Introduction**

Part 2 illustrates a Data Science 'Learning' technique which can be applied in different Knowledge Applications. Note that this example does not require in-depth knowledge in Data Science. 

\*\*\*\*

**Basic Learning Technique \(Passive\)**

Story:  Persona is a chain restaurant owner who is interested in knowing how his customers feel about his restaurant... This person went to Yelp to see the reviews written on his restaurant. He got the data from the internet, someone helped me crawl this website and extract my reviews. 

I decided to classify these reviews into 2 groups, positive and negative. This is, I made reviews with more than 4 stars positive and those with less than that as negative. 

I decided to train a Machine Learning model based on this dataset which I consider accurate. 

A data scientist recommended to use Logistic Regression for this analysis. I created a function to train this model. The ID is the version. Every time I hit run, there will be a prediction model created. that fits my training data set. 

67% is better than random guessing... 

2nd STEP - Evaluate

The restaurant owner gets involved again, he looks at the Evaluate Function and then what... It requires version ID number, run it.... Evaluate the model on Test, the dataset is small... 

3rd Step predictOne

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



