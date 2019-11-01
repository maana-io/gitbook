# Learning

---------------------------------------------------------------------------------------------------------------**Material Development Checklist**

* [ ] Power Point Slides \(**pending - check if needed**\)
* [ ] Workspaces \([https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases](https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases)**\)**
* [ ] Step-by-Step Instructions for Learning Assistant \(**pending**\)
* [ ] Case description \(**pending**\)

---------------------------------------------------------------------------------------------------------------

Link to Workspace: [https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases](https://app.gitbook.com/@maana/s/q/v/3.2.1/training/basics/basic-orientation/use-cases)



Use case description: 



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
3. Let the model makes prediction on a pool of unlabeled data to evaluate itself. 
4. Let the model asks SMEs for help \(student to teacher approach\)
   * option 1: the model asks random questions from the pool of unlabeled data. 
   * option 2: the model asks "smart" questions \(based on active learning technique\).
5. SMEs answer questions. 
6. Retrain the model. 
7. Reevaluate the model to see how SME feedback helps.

      The point here is to show that asking "smart" questions can improve model quality faster than asking random questions. 



Text classification, e.g. 

1. Given a piece of text \(e.g. a sentence, a short paragraph\), predict the "class" of the text. 
2. The classes are data dependent. Could be "Positive", "Negative" for customer review data. Could be "High Risk", "Low Risk", "Medium Risk" for risk data. 
3. The use case is populated with 1000 Yelp reviews, with Positive and Negative labels. \(Other datasets, such as IMDB movie review, are available and can be selected\)



