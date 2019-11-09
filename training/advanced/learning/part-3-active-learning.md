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



