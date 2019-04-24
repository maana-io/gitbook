# Curate Kinds

\[TBD\]

The loader then creates a new Kind, "MvApiListCSV," that provides an _interpretation_ of the raw data. Its structure mirrors that of the file and its instances are indexed in KindDB.

If there is a problem with the interpretation, the File Kind is marked in error and you may be able to take corrective steps.

As the Kind and its instances are loaded into the KindDB, various "bots" will begin indexing and mining the content to extract meaning and connect to existing Knowledge Graphs

The "raw data" and its "raw interpretation" represent a ground truth. However, it is likely you will want to improve the Kind and Field names, manage connections to other KGs, and create new Kinds from one or more Fields.

The bots will also produce subsequent interpretations and connections from the interpreted Kind. These include:

* Field classifications: interpretation of individual fields and their values against known Kinds and instances \(e.g., People, Places, Organizations, Categorical\)
* Entity extraction: analysis of comments, descriptions, or whole documents to identify mentions of entities, values, and facts
* Text classification: classification of comments, descriptions, or whole documents into preferred groups \(e.g. Comment problem types - Stuck pipe, Waiting on weather, etc. or document types - AFE report or Lease agreement\)

#### Rename a Kind <a id="UseCase03:CurateKinds-RenameaKind"></a>

#### Rename a Field <a id="UseCase03:CurateKinds-RenameaField"></a>

#### Coerce a Field type <a id="UseCase03:CurateKinds-CoerceaFieldtype"></a>

#### Accept/reject a recommended scalar field type  <a id="UseCase03:CurateKinds-Accept/rejectarecommendedscalarfieldtype"></a>

#### Accept/reject a recommended categorical field type  <a id="UseCase03:CurateKinds-Accept/rejectarecommendedcategoricalfieldtype"></a>

#### Accept/reject a recommended relation  <a id="UseCase03:CurateKinds-Accept/rejectarecommendedrelation"></a>

* Configure resolution strategy
* Map additional fields

### Steps <a id="UseCase03:CurateKinds-Steps"></a>

1. Select the interpreted Kind, "MvApiListCSV" in the Explorer or in the Knowledge Graph 
2. Rename this kind to "Well"
3. Navigate to the Info tab in the Context panel. Click on edit schema and select the Field you wish to modify/look at classifier suggestions.
4. You can select from a list of "suggested types" \(currently scalar types or regular expression matches\), Kinds \(available in your Workspace\) and Scalars 
5. Once you are done, hit save \(to save changes\) or cancel \(to stick with current selection\) and exit schema editor
6. If changed, the new Field type should be reflected in the expanded Kind view on the KG

