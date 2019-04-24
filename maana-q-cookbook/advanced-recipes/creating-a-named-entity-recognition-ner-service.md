# Creating a Named Entity Recognition \(NER\) Service

## About this Tutorial <a id="about-this-tutorial"></a>

The Maana-NER-service is for identifying entities in text and identifying their location within that text. It using two approaches:

* **Stochastic method** - Stanford CRF Classifier \(Conditional Random Field: [https://en.wikipedia.org/wiki/Conditional\_random\_field](https://en.wikipedia.org/wiki/Conditional_random_field)\) and
* **Deterministic method** - Tokens Regex: [https://stanfordnlp.github.io/CoreNLP/tokensregex.html](https://stanfordnlp.github.io/CoreNLP/tokensregex.html)​

### What the Service is Used For <a id="what-the-service-is-used-for"></a>

In particular, the service uses a stochastic approach so it can identify entities that are not explicitly present in the training set. For example, it could identify "Zack" as a name, even if "Zack" is not mentioned in the training data. The approach being used takes into account the context of words in a sentence to determine if they belong to a particular class of entity.

#### Detected Entities: <a id="detected-entities"></a>

| n | Entity | CRF | Regex |
| :--- | :--- | :--- | :--- |
| 01 | DateKind | + | + |
| 02 | TimeKind | + | + |
| 03 | Person | + | - |
| 04 | Location | + | - |
| 05 | Organization | + | - |
| 06 | Currency | + | - |
| 07 | Number | + | - |
| 08 | Percentage | + | - |
| 09 | URL | - | + |
| 10 | Email | - | + |
| 11 | PhoneNumber | - | + |
| 12 | SocialSecurityNumber | - | + |
| 13 | IpAddress | - | + |
| 14 | WebLink | - | + |
| 15 | GeoCoordinate | - | + |

### When to Use It <a id="when-to-use-it"></a>

This service is important as part of a pipeline where:

1. Simply identify what text contains a particular entity.
2. Detect multiple entities in text - this could be used in co occurrence computations where you want to identify a person along with a well type.
3. The entities can be used as part of a pipeline in a larger pattern matching scheme - for example to identify phrases that have a person followed by a date \(and then extract additional information using pattern based methods\).
4. As a first step in an information extraction pipeline to help fill in tables.

## Examples of How to Use the Service - Example queries <a id="examples-of-how-to-use-the-service-example-queries"></a>

### Ex 1. Extract <a id="ex-1-extract"></a>

Examples of "extract" query to run with default Model.

```text
query Extract {
  extract(
    sources: [
      "John, please get that article on www.linkedin.com or https://google.com or 192.67.23.222
      and files: bla123bla.doc and itisme.jpg
      and send to me by 5:00PM on Jul 4th 2018 or 4:00 am on 01/09/12 would be ideal, actually.
      If you have any questions about \"Microsoft\" or 'Google' office at \"New York\"
      you can reach my associate at (012)-345-6789 or (230) 241 2422 or +1(345)876-7554 or associative@mail.com or &lt;abracadabra123@maana.io>.
      Send me $5,987.56 or £4,123.14 or € 100 by PayPal.
      My SSN is 456-23-0965
      My coordinates are: 47.617640, -122.191905 or 47°37'03.5\"N 122°11'30.9\"W"
    ]
  ) {
    entityName
    surfaceForm
    fromSpan
    fromOffset
  }
}
```

#### Output results <a id="output-results"></a>

```text
{
  "data": {
    "extract": [
      {
        "entityName": "Person",
        "surfaceForm": "John",
        "fromSpan": "4",
        "fromOffset": "0"
      },
      {
        "entityName": "URL",
        "surfaceForm": "www.linkedin.com",
        "fromSpan": "16",
        "fromOffset": "33"
      },
      {
        "entityName": "URL",
        "surfaceForm": "https://google.com",
        "fromSpan": "18",
        "fromOffset": "53"
      },
      {
        "entityName": "IpAddress",
        "surfaceForm": "192.67.23.222",
        "fromSpan": "13",
        "fromOffset": "75"
      },
      {
        "entityName": "TimeKind",
        "surfaceForm": "5:00PM on",
        "fromSpan": "9",
        "fromOffset": "147"
      },
      {
        "entityName": "DateKind",
        "surfaceForm": "Jul 4th 2018",
        "fromSpan": "12",
        "fromOffset": "157"
      },
      {
        "entityName": "TimeKind",
        "surfaceForm": "4:00 am on",
        "fromSpan": "10",
        "fromOffset": "173"
      },
      {
        "entityName": "DateKind",
        "surfaceForm": "01/09/12",
        "fromSpan": "8",
        "fromOffset": "184"
      },
      {
        "entityName": "Organization",
        "surfaceForm": "Microsoft",
        "fromSpan": "9",
        "fromOffset": "252"
      },
      {
        "entityName": "Organization",
        "surfaceForm": "Google",
        "fromSpan": "6",
        "fromOffset": "267"
      },
      {
        "entityName": "Location",
        "surfaceForm": "New York",
        "fromSpan": "8",
        "fromOffset": "286"
      },
      {
        "entityName": "PhoneNumber",
        "surfaceForm": "(012)-345-6789",
        "fromSpan": "14",
        "fromOffset": "326"
      },
      {
        "entityName": "PhoneNumber",
        "surfaceForm": "(230) 241 2422",
        "fromSpan": "14",
        "fromOffset": "344"
      },
      {
        "entityName": "PhoneNumber",
        "surfaceForm": "+1(345)876-7554",
        "fromSpan": "15",
        "fromOffset": "362"
      },
      {
        "entityName": "Email",
        "surfaceForm": "associative@mail.com",
        "fromSpan": "20",
        "fromOffset": "381"
      },
      {
        "entityName": "Currency",
        "surfaceForm": "$5,987.56",
        "fromSpan": "9",
        "fromOffset": "443"
      },
      {
        "entityName": "Currency",
        "surfaceForm": "£4,123.14",
        "fromSpan": "9",
        "fromOffset": "456"
      },
      {
        "entityName": "Currency",
        "surfaceForm": "€ 100",
        "fromSpan": "5",
        "fromOffset": "469"
      },
      {
        "entityName": "Organization",
        "surfaceForm": "PayPal",
        "fromSpan": "6",
        "fromOffset": "478"
      },
      {
        "entityName": "SocialSecurityNumber",
        "surfaceForm": "456-23-0965",
        "fromSpan": "11",
        "fromOffset": "496"
      },
      {
        "entityName": "GeoCoordinate",
        "surfaceForm": "47.617640, -122.191905",
        "fromSpan": "22",
        "fromOffset": "528"
      },
      {
        "entityName": "GeoCoordinate",
        "surfaceForm": "47°37'03.5\"N 122°11'30.9\"W",
        "fromSpan": "26",
        "fromOffset": "554"
      }
    ]
  }
}
```

### Ex 2. Extract with customer Model or Token-Regex rules <a id="ex-2-extract-with-customer-model-or-token-regex-rules"></a>

Example of extract query to run with customer model. It returns an array of entities. You can drag & drop you crf model file to Maana, copy url, uncomment model URL and paste into query.

```text
query ExtractWithModelOrRegex {
  extract(
    source: "Daily update notification made to BSEE Houma District, Bobby Nelson." #, modelURL: "http://.../your_awesome_crf_model.ser.gz"
  ) {
    fromSpan
    fromOffset
    entityName
    surfaceForm
  }
}
```

#### Output results <a id="output-results-1"></a>

```text
{
  "data": {
    "extract": [
      {
        "entityName": "Organization",
        "surfaceForm": "BSEE",
        "fromSpan": "4",
        "fromOffset": "34"
      },
      {
        "entityName": "Location",
        "surfaceForm": "Houma District",
        "fromSpan": "14",
        "fromOffset": "39"
      },
      {
        "entityName": "Person",
        "surfaceForm": "Bobby Nelson",
        "fromSpan": "12",
        "fromOffset": "55"
      }
    ]
  }
}

```

There is also a capability to use customer’s Token-Regex rules if specify path to Regex.rules in modelURL parameter.

### Ex 3. Batch Extract <a id="ex-3-batch-extract"></a>

Example of "batch extract" query - it takes a list of source text and returns an array of array of entities, one array for each source.

```text
query BatchExtract {
  extractBatch(
    sources: [
      "Received verbal approval from Casey Kavanaugh (BSEE Houma District) on 10/8/12 @ 2:01 pm"
      "David Stanley lives in Lake Charles and works for MMS."
    ] #, modelURL: "http://.../your_awesome_crf_model.ser.gz"
  ) {
    fromSpan
    fromOffset
    entityName
    surfaceForm
  }
}
```

#### Output results <a id="output-results-2"></a>

```text
{
  "data": {
    "extractBatch": [
      [
        {
          "entityName": "Person",
          "surfaceForm": "Casey Kavanaugh",
          "fromSpan": "15",
          "fromOffset": "30"
        },
        {
          "entityName": "Organization",
          "surfaceForm": "BSEE",
          "fromSpan": "4",
          "fromOffset": "47"
        },
        {
          "entityName": "Location",
          "surfaceForm": "Houma District",
          "fromSpan": "14",
          "fromOffset": "52"
        },
        {
          "entityName": "DateKind",
          "surfaceForm": "10/8/12",
          "fromSpan": "7",
          "fromOffset": "71"
        },
        {
          "entityName": "TimeKind",
          "surfaceForm": "2:01 pm",
          "fromSpan": "7",
          "fromOffset": "81"
        }
      ],
      [
        {
          "entityName": "Person",
          "surfaceForm": "David Stanley",
          "fromSpan": "13",
          "fromOffset": "0"
        },
        {
          "entityName": "Location",
          "surfaceForm": "Lake Charles",
          "fromSpan": "12",
          "fromOffset": "23"
        },
        {
          "entityName": "Organization",
          "surfaceForm": "MMS",
          "fromSpan": "3",
          "fromOffset": "50"
        }
      ]
    ]
  }
}
```

### Ex 4. Is Surface Form <a id="ex-4-is-surface-form"></a>

Example of "is surface form" query - returns true if a particular source is exactly a surface form of "entityName"

```text
query IsSurfaceForm {
  isSurfaceForm(source: "Seattle", entityName: "Location")
}
```

#### Output results <a id="output-results-3"></a>

```text
{
  "data": {
    "isSurfaceForm": true
  }
}
```

### Ex 5. Is Surface Form with customer Model <a id="ex-5-is-surface-form-with-customer-model"></a>

```text
query IsSurfaceFormWithModel {
  isSurfaceForm(
    source: "BOEM"
    entityName: "Organization"
    #, modelURL: "http://.../your_awesome_crf_model.ser.gz"
  )
}
```

#### Output results <a id="output-results-4"></a>

```text
{
  "data": {
    "isSurfaceForm": true
  }
}
```

### Ex 6. Parse <a id="ex-6-parse"></a>

Example of parse query:

* returns the parsed entity name if the source text is exactly as entity with no additional text to the left or right of the entity,
* otherwise return empty string.

```text
query Parse {
  parse(
    source: "Forrest Gump"
    #, modelURL: "http://.../your_awesome_crf_model.ser.gz"
  )
}
```

#### Output results <a id="output-results-5"></a>

```text
{
  "data": {
    "parse": "Forrest Gump"
  }
}
```

```text
query Parse {
  parse(
    source: "I visited my friend Forrest Gump"
    #, modelURL: "http://.../your_awesome_crf_model.ser.gz"
  )
}
```

#### Output results <a id="output-results-6"></a>

```text
{
  "data": {
    "parse": ""
  }
}
```

## Using Service Functions with Maana <a id="using-service-functions-with-maana"></a>

1. Create new Workspace and expand 'Inventory' \(bottom left\).

![Figure 1: Expend &apos;Inventory&apos;: &apos;Services&apos; -&amp;gt; &apos;Maana Natural Language Processing&apos;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFJMQkMKnHD_W_wdc%2Fimage.png?alt=media&token=0576e337-a37f-4932-8fa8-0a9a7647e77f)

2. Then drag & drop any service function to your workspace canvas.

### Extract <a id="extract"></a>

1. Drag & drop 'extract' function. On the canvas you'll see new Kind - Extract function Kind.

![Figure 2: Extract function Kind](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFQoPM_tGZK4QFybg%2Fimage.png?alt=media&token=527078fa-ca86-41e3-a372-c2372f8e4b09)

2. Click on 'triangle in circle' at the bottom of thin vertical bar on the right \(see Figure 3\).

* Type your text into 'source' field.
* As an option, you can define CRF Model by typing modelURL and marked check box. Before it you need to drag & drop your CRF Model to canvas and copy URL \(on the right\).

![Figure 3: To extract entities click &apos;RUN&apos; button.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFVQQXtVOMM2lxEnQ%2Fimage.png?alt=media&token=fbb7aa1d-0bc9-409b-aeda-1d41203239a9)

3. You will see the results \(extracted entities\) in the bottom section.

![Figure 4: Results of extraction \(click to expand blue triangles\).](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFZP5y9NuQ1TG-JpW%2Fimage.png?alt=media&token=0ed35b2c-1158-49e7-8509-eaa48a6b96a3)

### isSurfaceForm <a id="issurfaceform"></a>

1. Drag & drop 'isSurfaceForm' function. On the canvas you'll see new Kind - isSurfaceForm function Kind.
2. Click on 'triangle in circle' at the bottom of thin vertical bar on the right.
3. Type your entity in 'source' field.
4. Type expected entity name in 'entityName' field \(see all entity names in paragraph "Detected Entities" in this tutorial above\).
5. Define 'modelURL' if you want to.
6. Click 'RUN' button. See results in the bottom section.

![Figure 5: To detect is it surface form click &apos;RUN&apos; button.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFhyRb2Q3yCDeT-lc%2Fimage.png?alt=media&token=c6014d60-6960-4828-989a-7d44513271df)

![Figure 6: Results of &apos;Microsoft&apos; is surface form of &apos;Organization&apos; type. parse](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFddiDn8ID5PFTRe7%2Fimage.png?alt=media&token=af926fdf-1507-4364-9e67-43a338344474)

### Parse <a id="parse"></a>

1. Drag & drop 'parse' function. On the canvas you'll see new Kind - parse function Kind.
2. Click on 'triangle in circle' at the bottom of thin vertical bar on the right.
3. Type your entity in 'source' field.
4. Define 'modelURL' if you want to.
5. Click 'RUN' button. See results in the bottom section.

![Figure 7: To parse entity click &apos;RUN&apos; button.](../../.gitbook/assets/image%20%2893%29.png)

![Figure 8: Results of parsing &apos;Forrest Gump&apos; entity.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXLCc4jXsfA8RJIfAw4%2F-LXLFrp8njbITMWX5aGV%2Fimage.png?alt=media&token=dce57401-45ac-48d3-9a29-6c64664f4aa7)

