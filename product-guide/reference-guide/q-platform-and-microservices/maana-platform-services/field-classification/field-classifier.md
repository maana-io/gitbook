# Field Classifier Service

### What is this service? <a id="FieldClassifierService-Whatistheservicefor?"></a>

The field classifier operates on uploaded tabular files, such as CSV files.  The  classifier looks at the contents of columns of the tabular data and classifies the column \(Field\) along with a confidence score, among several different types.  The possible classifications are 

* BooleanKind
* Number
* Currency
* Email
* IpAddress
* PhoneNumber
* URL
* TimeKind
* DateKind
* SocialSecurityNumber
* GeoCoordinate
* Latitude
* Longitude
* DocFile
* USState
* CountryCode
* Person
* Location
* Organization
* PhysicalQuantity
* Text

### When might you want to use it? <a id="FieldClassifierService-Whenmightyouwanttouseit?"></a>

You might want to know whether fields can be classified as one of the standard types provided. This is particularly important for services that operate on specific types of fields such as the [Entity Extractor]() \(which only applies to Text fields\) or the [Meta-Learning]() classification service, which needs to know the type of data it is operating on. In addition, it can be useful in more generic data retrieval. The classification score indicates the fraction of entries of a given type which may be helpful if the results are not what is expected. An example would be if 50% of the entries were emails and the other 50% were phone numbers under the field "contact info".

### How do you run/invoke it? <a id="FieldClassifierService-Howdoyourun/invokeit?"></a>

The field classification service runs automatically when data is uploaded \(by responding to the [`hasKind` event](../data-loader.md) \[TBD\]_where will We Explain Eventing?_\). Alternatively, the service can be imported to a workspace and used in [function composition]().

### GraphQL interface

The following queries and mutations are currently implemented:

Return the field classification for a given kind with kind id given by id. The return ids are the field ids while name is the name of the field and score is the confidence score of a given classification.

#### fieldClassifications

```
query {
  fieldClassifications(id: "295ac75b-54d2-4b51-9562-8ecd92808a42") {
    name
    id
    score
  }
}
```

#### classifyFields

Classify the fields of a kind and kickoff and publish a 'fieldClassified' event \[TBD\]_Eventing Link_. Again, id in the classifyFields function is the kindId. This mutation returns a [Bot Action]().

```
mutation {
  classifyFields(kindId: "295ac75b-54d2-4b51-9562-8ecd92808a42") {
    id
    created
    lastUpdated
    status
    errors
    service
  }
}
```

#### copyFieldAsKind

This query copies a field and creates a new column with the specific Kind chosen - basically is typecasting and creating a new column with that type. The instances of that field are stored in the actual kind.

copyFieldAsKind takes the following parameters

* kindId - the id of the kind containing the columns of interest
* fieldName - the field name of the field we will be copying
* newFieldName - the name of the field we want to copy this to \(cannot exist yet since it is being created\)
* newFieldKind - the kind of the new field. Must be a kind from field classifier, Person, Email, Location, Organization ...
* newFieldKindId - alternatively, the id of the above kind
* forceAll - must be true or false. If true it copies all instance to the new field, if false, it only copies those instances which are actually classified as "newFieldKind"

An example mutation is shown below. `testDataKind` is a CSV file kind in which the column "C3" has been classified as a "PhoneNumber" and now can be added onto the PhoneNumber Kind. 

```
mutation {
  copyFieldAsKind(
    kindId: testDataKindId
    fieldName: "C3"
    newFieldName: "C3awesome"
    newFieldKind: "PhoneNumber"
    forceAll: true
  )
}
```

After this mutation is performed you will expect

1. A new column called "C3awesome" will be in the testDataKind
2. The contents of "C3awesome" will be ids
3. The contents of the kind "PhoneNumber" will be the contents of the column "C3" in the testDataKind
4. The instance ids of PhoneNumber will be the iids found in "C3awesome"

If you run the exact same query a second time, it will most likely fail since the column has already been created. If you run it a second time, just change the name of "newFieldName"

Field Classifier comes with a [visual assistant]() to display classifications and run the `copyFieldsAsKinds` mutation

### How do you see results? <a id="FieldClassifierService-Howdoyouseeresults?"></a>

After a CSV file is uploaded and the CSV Kind clicked, links to the given classifications will be shown on the right hand side column.  In addition by scrolling down on the right hand side column, one can click on the 'edit' button and select the field dropdown filter, by deleting the default entry \(often STRING\) the rest of the possible types will appear, including those above.

### How does the service work? <a id="FieldClassifierService-Howdoestheservicework?"></a>

The service uses a combination of regex and results from the ner-service to classify fields.

## Field Classifier \(Assistant\) Inside the Platform <a id="field-classifier-assistant-inside-the-platform"></a>

In simple terms, the Field Classifier\(FC\) Assistant provides a visual guide to see how FC has classified the fields of a csv. Moreover, it gives the option of running the `copyFieldAsKind` mutation on the classified fields \(either on the entire field, or only those instances that satisfy a given classification\).

* To start with, upload a CSV file, in this case we use [operator](https://github.com/maana-io/q-tutorials/blob/master/maana-fieldclassifier/operator.csv).
* Load the data into the platform. Bring the Kind for the operator.csv file into the workspace by clicking the link on the bottom of operator.csv - the Kind will be called "OperatorCSV".
* As soon as the CSV file is uploaded the field classifier is kicked off and classifications for each of the columns of the tabular data are produced.
* Possible classifications will show up as links in the "OperatorCSV" kind.
* Critically, the data has two interesting classifications, "Person" and "Organization" for the fields "contact" and "business".

![Figure 1: View after uploading CSV and Clicking on kind link](https://maanaimages.blob.core.windows.net/maana-q-documentation/f1.png)

* Make sure the "OperatorCSV" is selected then in the assistants panel, select "Maana Field Classifier", this brings up the user interface for the field classifier. In the upper left hand corner it should say "OperatorCSV".

![Figure 2: Field Classifier Assistant applied to OperatorCSV kind](https://maanaimages.blob.core.windows.net/maana-q-documentation/f2.png)

* Scroll down to the fieldId "contact".
* To the right there should be a "proposedType" of "Person" along with 2 buttons, "Add All" and "Add Matching".
* When you click on one of these buttons it creates a new column of the "OperatorCSV" kind with the name "contactPerson" which is the concatenation of the original field name "contact" and the strong type "Person".
  * The "Add All" button adds all the data in the "contact" column to the new column "contactPerson".
  * The "Add Matching" button adds only the data that is classified as type "Person" to the "contactPerson" column - all other non matching records are empty.

There are also additional fields, the "Type" field is the original graphql type - STRING, FLOAT, BOOLEAN etc...

* The ProposedType can contain any of the types available as classifications from the field classifier.
* The Percent column gives an estimate of the percentage of records that matched a given classification, this is an estimate as only 1000 columns of the original data are used to produce the estimate.
* When the "Add Matching" or "Add All" buttons are clicked the data from "contact" say, is added to the "Person" kind inside Maana. The Ids for those instances are stored in the new "contactPerson" column. In this way, multiple different kinds can refer to the same "Person," we then have a common location for "Person" data and associations between different data sources.

![Figure 3: A new column is added to OperatorCSV with Ids to the Person kind.](https://maanaimages.blob.core.windows.net/maana-q-documentation/f3.png)

![Figure 4: The Person kind is populated with new entries from the OperatorCSV &quot;contact&quot; field.](https://maanaimages.blob.core.windows.net/maana-q-documentation/f4.png)

### More Information

See the Maana Cookbook for a tutorial on how to use [FC Service and Assistant together](https://maana.gitbook.io/q/maana-q-cookbook/advanced-recipes/field-classifier/field-classifier-and-assistant-tutorial).   
For general information about Service Assistants, see [this page](https://maana.gitbook.io/q/product-guide/reference-guide/technical-design-and-architecture/bot-actions/bots-for-assistants-requirements) on Platform Capabilities and Architecture. 

