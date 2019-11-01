# Learning

---------------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [ ] Power Point Slides \(**pending - check if needed**\)
* [ ] Workspaces **\(WIP\)**
* [ ] Step-by-Step Instructions for Learning Assistant \(**pending**\)
* [ ] Case description \(**pending**\)

---------------------------------------------------------------------------------------------------------------

Link to Workspace: [https://cstraining01.knowledge.maana.io/workspace/512a43c7-660c-43d8-b525-42ab0c1a5a61](https://cstraining01.knowledge.maana.io/workspace/512a43c7-660c-43d8-b525-42ab0c1a5a61)

Use case description: 



Training goals:

1. Show how SME feedback loop works:

* Prepare labeled data, unlabeled data, and test data. 
* Train a model.
* Evaluate the model on test data. Figure out mistakes the model made. 
* SMEs give feedback to the model \(teacher to student approach\) 
* Retrain the model. 
* Reevaluate the model to see how SME feedback helps.
* The loop continues.

      The point here is to show that SME feedback can improve model quality.

2. Show how active learning can improve the model faster, with less effort from SMEs.

* Prepare labeled data, unlabeled data, and test data. 
* Train a model.
* Let the model makes prediction on a pool of unlabeled data to evaluate itself. 
* Let the model asks SMEs for help \(student to teacher approach\)
  * option 1: the model asks random questions from the pool of unlabeled data. 
  * option 2: the model asks "smart" questions \(based on active learning technique\).
* SMEs answer questions. 
* Retrain the model. 
* Reevaluate the model to see how SME feedback helps.

      The point here is to show that asking "smart" questions can improve model quality faster than asking random questions. 



Text classification, e.g. 

* Given a piece of text \(e.g. a sentence, a short paragraph\), predict the "class" of the text. 
* The classes are data dependent. Could be "Positive", "Negative" for customer review data. Could be "High Risk", "Low Risk", "Medium Risk" for risk data. 
* The use case is populated with 1000 Yelp reviews, with Positive and Negative labels. \(Other datasets, such as IMDB movie review, are available and can be selected\)



