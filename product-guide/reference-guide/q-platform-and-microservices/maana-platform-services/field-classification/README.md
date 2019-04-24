# Field Classification

The Field Classifier Service and Field Classifier Assistant are tools for setting strong types for columns of tabular data inside Maana. A column of data might contain names of people, but has the column name "contact." The field classifier can identify recommended classifications for this type of data and then the user can select a type to enforce its classification. The strongly typed column is then ready to be used in services that only operate on specific types and/or be part of a larger logic and reasoning process.

Currently:

* [Field classifier](https://maana-ue.gitbook.io/product/~/drafts/-LZph7cZfruBt7FBiKE8/primary/cookbook/q-tutorials/field-classifier) analyzes the full set of data
* Generate a set of classes \(Kinds\) and their scores
* The field can be updated to one of these classifications \(Kinds\)

Proposed extension:

**Instead of** _**converting**_ **the field type, allow adding new fields for each Kind and materialize/index the subset of values \(ids\).**

In other words, if WorkOrderCSV { contactName:String }  is classified as Person, Location, and Phone Number, then instead of changing the field from string to one of these Kinds, allow the user to add a field for each one, such that WordOrderCSV { contactPerson:Person contactLocation:Location, contactPhoneNumber: PhoneNumber } and the values \(or their resolved identities\) from contentNamethat classify as such are materialized.

The [Field Classifier Assistant]() provides a UI to preview those values that classify as the various Kinds before committing to the decision \(to verify or possibly cleanse\).  


