# Assistant Tutorial

  
The Field Classifier Service and Field Classifier Assistant are tools for setting strong types for columns of tabular data inside Maana. A column of data might contain names of people, but has the column name "contact." The field classifier can identify recommended classifications for this type of data and then the user can select a type to enforce its classification. The strongly typed column is then ready to be used in services that only operate on specific types and/or be part of a larger logic and reasoning process.

{% file src="../../../.gitbook/assets/operators.csv" caption="operator.csv; the file used in this tutorial" %}

## Field Classifier \(Assistant\) <a id="field-classifier-assistant-inside-the-platform"></a>

* To start with, upload a CSV file, in this case we use operator.csv \(attached above\).
* Load the data into the platform. Bring the Kind for the operator.csv file into the workspace by clicking the link on the bottom of operator.csv - the Kind will be called "OperatorCSV".
* As soon as the CSV file is uploaded the field classifier is kicked off and classifications for each of the columns of the tabular data are produced.
* Possible classifications will show up as links in the "OperatorCSV" kind.
* Critically, the data has two interesting classifications, "Person" and "Organization" for the fields "contact" and "business".

![Figure 1: View after uploading CSV and Clicking on kind link](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LWw6tnPhfTFBfqSswID%2F-LWw7YSe2ETAFDbuHDqo%2Fimage.png?alt=media&token=be11a8cf-53ef-4607-ba63-97fd51a7da79)

* Make sure the "OperatorCSV" is selected then in the assistants panel, select "Maana Field Classifier", this brings up the user interface for the field classifier. In the upper left hand corner it should say "OperatorCSV".



![Figure 2: Field Classifier Assistant applied to OperatorCSV kind](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LWw6tnPhfTFBfqSswID%2F-LWw7jFS2Y92k1gE4Q1R%2Fimage.png?alt=media&token=3c32ef7d-7a9b-4b2b-bc64-ba9ef354727d)

* Scroll down to the fieldId "contact".
* To the right there should be a "proposedType" of "Person" along with 2 buttons, "Add All" and "Add Matching".
* When you click on one of these buttons it creates a new column of the "OperatorCSV" kind with the name "contactPerson" which is the concatenation of the original field name "contact" and the strong type "Person".
  * The "Add All" button adds all the data in the "contact" column to the new column "contactPerson".
  * The "Add Matching" button adds only the data that is classified as type "Person" to the "contactPerson" column - all other non matching records are empty.

There are also additional fields, the "Type" field is the original graphql type - STRING, FLOAT, BOOLEAN etc...

* The ProposedType can contain any of the types available as classifications from the field classifier.
* The Percent column gives an estimate of the percentage of records that matched a given classification, this is an estimate as only 1000 columns of the original data are used to produce the estimate.
* When the "Add Matching" or "Add All" buttons are clicked the data from "contact" say, is added to the "Person" kind inside Maana. The Ids for those instances are stored in the new "contactPerson" column. In this way, multiple different kinds can refer to the same "Person," we then have a common location for "Person" data and associations between different data sources.

![Figure 3: A new column is added to OperatorCSV with Ids to the Person kind](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LWw6tnPhfTFBfqSswID%2F-LWw7qdXLSpqr0dK7wZe%2Fimage.png?alt=media&token=7392d4bd-b1e7-476b-8ecb-d54e2a9dfe52)

![Figure 4: The Person kind is populated with new entries from the OperatorCSV &quot;contact&quot; field.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LWw6tnPhfTFBfqSswID%2F-LWw807PZBEg2uSAJh3c%2Fimage.png?alt=media&token=bc006eed-7a16-4bd9-a3fe-5864b3d9c603)

