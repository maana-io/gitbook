# Learning

-------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [ ] Power Point Slides \(**pending - check if needed**\)
* [ ] Workspaces \([https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases](https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases)**\)**
* [ ] Step-by-Step Instructions for Learning Assistant \(**pending**\)
* [ ] Case description \(**pending**\)

-------------------------------------------------------------------------------------------------------

### Use case description: 

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



