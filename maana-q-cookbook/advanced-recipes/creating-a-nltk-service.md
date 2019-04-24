# Creating a NLTK service

## About this Tutorial

This is a template for creating a Maana Knowledge Service in Python. 

{% hint style="info" %}
This requires python 3.6+.
{% endhint %}

## Installation

1. To install the python packages required, run this:

```text
pip install -r requirements.txt
```

2. Open python and run these commands:

```text
import nltk
nltk.download()
```

3. At the prompt, download 'all'.

## Starting

```text
python server.py
```

## Practice Queries

### Adds a sentence

`curl -XPOST http://localhost:7357/graphql -H 'Content-Type: application/json' -d '{"query": "mutation { addSentence(input:{id: \"1\", text: \"this is a sentence\"}) { id } }"}'`

### Gets all sentences

```text
``` curl -X POST -H "Content-Type: application/json" -d '{ "query": "{ allSentences { text } }" }' 
http://localhost:7357/graphql
```

This will also automatically parse a the first column of a csv added for text and add sentences using NLTK. Drop a csv where the first column is just text, and it will parse through it all and add them to the sentences kind!

