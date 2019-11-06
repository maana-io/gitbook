# Fact Recognition and FR-Bot

## What is Fact Recognition Service? <a id="what-is-fact-recognition-service"></a>

This service is used for extracting relations, or facts or triples, from text. The service is based on Stanford CoreNLP's Information Extraction library \([https://nlp.stanford.edu/software/openie.html](https://nlp.stanford.edu/software/openie.html)\).

This service could extract information from the phrase "Alex bought a bicycle for 50$." And store a series of triples "Alex", "bought", "bicycle" and "Alex", "bought a bicycle for", "50$". The extracted information can later be used for filling in tables or reasoning. The fact recognition service takes in a kind, a field name, and then set of patterns to perform Information Extraction.

Although Fact Recognition can perform triple extraction on a text input, it is a "pure logical service." This means that it does not have the capability to inspect kinds from -- or store its results to-- Maana. For that, the Fact Recognition Bot Service should be used. The FR-Bot Service coordinates the logic of Fact Recognition with the other Kinds and abilities of the platform. For a practical example of how these two are used, see the [Fact Recognition Tutorials](https://maana.gitbook.io/q/~/drafts/-L_Q5gV0LFJTEe_bmaXC/primary/maana-q-cookbook/advanced-recipes/fact-recognition-tutorials) in Maana Cookbook.

### When might you want to use it <a id="when-might-you-want-to-use-it"></a>

You may want to use these services if have unstructured text and want to extract person names, locations, or organizations. In addition one can extract how people, locations, organizations ... are related to each other using the information extraction.

### How do you run/invoke it? <a id="how-do-you-run-invoke-it"></a>

As with other Maana Knowledge services the various queries of Fact Recognition can either be invoked explicitly through a graphiql interface, or be used as part of function composition, so the output of one query can be used as the input of another.

### Sample Queries from Fact Recognition Service <a id="sample-queries-from-fact-recognition-service"></a>

{% tabs %}
{% tab title="Query 1" %}
```
query {
    extractTriples(text: "Alex bought a bike") {
        predicatePhrase {
            value
        }
        subjectPhrase {
            value
        }
        objectPhrase{
            value
        }
    }
}
```
{% endtab %}

{% tab title="Result 1" %}
```
{
  "data": {
    "extractTriples": [
      {
        "predicatePhrase": {
          "value": "bought"
        },
        "subjectPhrase": {
          "value": "Alex"
        },
        "objectPhrase": {
          "value": "bike"
        }
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Query 2" %}
```
query {
    extractByPattern(text : "John went to Lynwood and bought a pizza", patterns : [{predicateLemmas : ["purchase"], subjectEntityPattern : ["ANY"], objectEntityPattern : ["ANY"]}]) {
    predicateMatch {
      snippet {
        value
      }
    }
    subjectMatch {
        snippet {
        value
      }

    }
    objectMatch {
        snippet {
        value
      }
    }
  }
}
```
{% endtab %}

{% tab title="Result 2" %}
```
{
  "data": {
    "extractByPattern": [
      {
        "predicateMatch": {
          "snippet": {
            "value": "bought"
          }
        },
        "subjectMatch": {
          "snippet": {
            "value": "John"
          }
        },
        "objectMatch": {
          "snippet": {
            "value": "pizza"
          }
        }
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Query 3" %}
```
query {
    extractByExample(example : "John went to safeway and bought a pizza in Lynwood", text : "Larry goes to Gerks and purchased a bike in Issaquah") {
        predicateCorrespondences {
            basePredicate
            targetPredicate
        }
        entityCorrespondences {
            baseEntity
            targetEntity
        }
        score
    }
}
```
{% endtab %}

{% tab title="Result 3" %}
```
{
    "data": {
        "extractByExample": [
        {
            "predicateCorrespondences": [
            {
                "basePredicate": "goes to",
                "targetPredicate": "went"
            },
            {
                "basePredicate": "purchased",
                "targetPredicate": "bought"
            },
            {
                "basePredicate": "purchased bike in",
                "targetPredicate": "bought pizza in"
            }
            ],
            "entityCorrespondences": [
            {
                "baseEntity": "Gerks",
                "targetEntity": "safeway"
            },
            {
                "baseEntity": "Issaquah",
                "targetEntity": "Lynwood"
            },
            {
                "baseEntity": "Larry",
                "targetEntity": "John"
            },
            {
                "baseEntity": "bike",
                "targetEntity": "pizza"
            }
            ],
            "score": 13.5
        }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### Assumptions for effective Fact Recognition

1. Unstructured text that obeys reasonable rules of grammar to enable the parsing of noun and verb phrases.
2. Facts are repeated in text to overcome the generally low recall and precision when working with dependency parsing due to challenges with natural language.

### Warnings

1. The extractByExample and extractByExampleKind are mutations still in research and development, and as such, with certain data, may become long-running. The use of these mutations should be done with caution. Future feature releases may address making them more performant and robust.

### More Information

For a practical walk-through of Fact Recognition Services, visit their [tutorial pages](https://maana.gitbook.io/q/maana-q-cookbook/advanced-recipes/creating-a-fact-recognition-bot) in the Maana Cookbook. 

