# Meta-Learning

### What is this service?

Maana Metalearning service allows one to automatically create machine learning models from data in Maana. It creates knowledge in the knowledge graph by having classifiers, featurizers and their attributes as first class citizens, allowing us to reason over them. This work is presented in the following papers:

F. Yang, D. Lyu, B. Liu, and S. Gustafson, Peorl: Integrating symbolic planning and hierarchical reinforcement learning for robust decision-making, International Joint Conference of Artificial Intelligence \(IJCAI\), 2018.

Fangkai Yang, Steven Gustafson, Alexander Elkholy, Daoming Lyu, and Bo Liu, Program search for machine learning pipelines leveraging symbolic planning and reinforcement learning, Genetic Programming Theory and Practice XVI \(Ann Arbor, USA\) \(Wolfgang Banzhaf, Leigh Sheneman, Lee Spector, and Bill Tozier, eds.\), Springer, 19-21 May 2018, Forthcoming.

### Assumptions about usage:

1. There is a labeled dataset for use.
2. The dataset has been cleaned, and the features are ready for usage.

### How do you run/invoke it?

The main interface to Maana Metalearning is through the graphIQL endpoint, which allows one to train a classi er from kinds which exist in Maana. For the rest of this section, assume a kind exists in Maana with a kind id, a number of fields which are features to train on, and a target feature to predict.

* accuracy: The minimum target accuracy to try to achieve. 
* kindId: The kind id of the data to train on which exists in Maana. 
* excludeFields: \(optional\) If there are any fields the user wishes to exclude from the feature set to train on, they are listed here. 
* featureFields: \(optional\) Opposite excludeFields, the user may specify only those elds which are to be trained on, rather than only those to exclude. 
* candidateModels: This is a list of classification algorithms to try. The models available are generally those in scikit learn\[9\]. candidatePreprocessors: This is a list of preprocessors to try, from scikit learn. Additionally, the preprocessor 'noop' is allowed, which specifies that no preprocessor is to be used. 
* folds: \(optional\) The number of cross-validation folds to use. Defaults to 10. 
* modelProfilingEpisode: This is the number of runs to do in phase 1. It is the number of times a pipeline is to be tried before moving on. Recommended is 4 
* modelSearchEpisode: This is the number of runs to do in phase 2. It is the number of times to test the chosen pipeline to find the best parameter set. Recommended is 8. 

Additionally, the process can be changed during run time. We allow the following mutations to control the flow of the algorithm:

* StopMetaLearningAndSaveBest: This will stop the entire process and save the best model it has found so far. 
* StopCurrentPhase: This will stop the current phase and move onto the next with the best pipeline it has found so far. 
* StopCurrentTasks: This will stop the current pipeline it is testing. If, for example, one classifier is taking much longer than expected, the user can stop the current process and move onto the next pipeline to test in whatever phase it is in. 
* ChangeFeaturizerSetting: This will allow the user to change what featurizers are being used in the process. 

### ExampleMutations

In this simple example,  a classifier is trained on a kind personal data to predict income bracket. 

{% tabs %}
{% tab title="Input 1" %}
```graphql
 mutation training
    {
      trainClassifierKind(
        input:
          {
            accuracy: 0.70,
            kindId: "52238b88-01c5-404a-96c9-9cf79ffd1786",
            labelField:"salary", # The field name in the kind to try and learn / predict.
            excludeFields:["id"], # Optionally specificy fields to exclude.
            # featureFields:["age","education","occupation","sex","nativecountry"], # Optionally choose only those fields to include
            featureTypes: ["interger", "categorical", "categorical", "categorical", "categorical", "categorical", "categorical", "categorical", "categorical", "categorical"],
            candidateModels: ["random_forest_classifier", "logistic_classifier"],
            candidatePreprocessors:["noop"],
            folds:10, # This is the number of cross validation folds to use. Default and a good pick is 10
            modelProfilingEpisodes:10,
            modelSearchEpisodes:50
          }
      )
    }
```
{% endtab %}

{% tab title="Output 1" %}
```graphql
{

   "data": {

    "trainClassifierKind": true

    }

}
```
{% endtab %}
{% endtabs %}

The saved model \(with `trainedModelId: "<modelId>"`is then used to classify a single instance of a person's data\)

{% tabs %}
{% tab title="Input 2" %}
```graphql
mutation classify_inst {

  classifyInstance(input: {

    trainedModelId: "<modelId>",

    data:["{\r\n\"age\":39,\r\n\"workclass\":\"State-gov\",\r\n\"education\":\"Bachelors\",\r\n\"maritalstatus\":\"Never-married\",\r\n\"race\":\"White\",\r\n\"sex\":\"Male\"\r\n}"]

  })

}
```
{% endtab %}

{% tab title="Output 2" %}
```graphql
{

  "data": {

    "classifyInstance": [

      "<=50K"

    ]

  }

}
```
{% endtab %}
{% endtabs %}

### More information

See the Maana Cookbook for a tutorial on [how to use Metalearning Service](https://maana.gitbook.io/q/maana-q-cookbook/advanced-recipes/meta-learning-tutorial).

