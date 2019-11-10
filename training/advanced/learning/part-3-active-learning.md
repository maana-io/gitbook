---
description: Advanced Learning technique explained through and example
---

# Part 3 - Active Learning

**Advanced Learning Technique \(Active\)**

After you train the model... 

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

