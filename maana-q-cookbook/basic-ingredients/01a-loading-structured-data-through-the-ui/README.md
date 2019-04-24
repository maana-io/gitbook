# Loading Structured Data through the UI

\[TBD\]

At the core of Maana is the KindDB, which stores and indexes GraphQL schema and instances. It is convenient to define types and generate instance data from existing sources.

### Create a new workspace <a id="UseCase01:LoadStructuredFile-Createanewworkspace"></a>

Within the Maana "Workspace" tab, create a new workspace:

* Select the **Workspaces** tab at the top of the Maana portal,
* Select the blue circle with the "**+**" icon in it located in the upper left of your screen.  Your screen should now display a new Workspace that you have created, named **Untitled**, similar to the one shown in the example found below.

![](../../../.gitbook/assets/image%20%288%29.png)

### Select the workspace <a id="UseCase01:LoadStructuredFile-Selecttheworkspace"></a>

By default, the new workspace will open and be selected in the Explorer

![](https://confluence.corp.maana.io/download/attachments/36995833/01.a%20Select%20Workspace.png?version=1&modificationDate=1518024165338&api=v2)

### Rename the workspace <a id="UseCase01:LoadStructuredFile-Renametheworkspace"></a>

give it the name "BOEM Raw Data"

![](https://confluence.corp.maana.io/download/attachments/36995833/01.a%20Rename%20Workspace.png?version=1&modificationDate=1518023485243&api=v2)

### Save the renamed workspace <a id="UseCase01:LoadStructuredFile-Savetherenamedworkspace"></a>

![](https://confluence.corp.maana.io/download/attachments/36995833/01.b%20Save%20Workspace.png?version=1&modificationDate=1518023866514&api=v2)

### Rename the Knowledge Graph <a id="UseCase01:LoadStructuredFile-RenametheKnowledgeGraph"></a>

"Core"

### Upload a file <a id="UseCase01:LoadStructuredFile-Uploadafile"></a>

Upload "BOEMData/APIRawData/mv\_api\_list.csv" by "drag-and-drop" or using the upload action in the Explorer

A File Kind instance will appear in the Explorer and on the current/default KG, representing the physical file and associated metadata \(e.g., URL, MIME type, size, status\)

If the file transfer is long, a progress indicator will be shown and cancellation action provided

![](../../../.gitbook/assets/image%20%2860%29.png)

#### Requirements <a id="UseCase01:LoadStructuredFile-Requirements"></a>

* Supported file types
* Logging and auditing
* Storage quotas
* Limits
  * Max files
  * Max file size
* Visual indicator of progress
* Visual indicator of success/failure
* Detailed information about state
* Corrective actions
* File is available in the Maana local store
* File instance is added to Kind File

#### Variations <a id="UseCase01:LoadStructuredFile-Variations"></a>

* File sources
  * local drive
  * network file store
  * URL
* Collections
  * One file
  * Multiple files
    * Same type
    * Different types
  * Folders
  * Archives \(zip\)
* Failures
  * Can't access source file
  * Network disconnect
  * Out of storage
  * clean up the Kind File
  * clean up the Maana data store
  * clean up the Kind

### Preview the file <a id="UseCase01:LoadStructuredFile-Previewthefile"></a>

Once the file has been transferred to temporary cloud storage, its contents can be previewed while it is being interpreted and loaded into KindDB by background processes

#### Variations <a id="UseCase01:LoadStructuredFile-Variations.1"></a>

* Analyst previews the file data and determines the file is incorrectly parsed
  * ?Analyst fixes the file and retries?
  * Analyst deletes the file

### Parsing the file <a id="UseCase01:LoadStructuredFile-Parsingthefile"></a>

If the file was successfully uploaded, then the \[loader service\]\(/docs/help/guide/ksvcs/io/maana/loader\) will attempt to interpret its structure and contents.

Kinds indicate when they are busy being processed or are in need of attention or correction. In this example, the BOEM data file is automatically recognized as a seperated-value file, its header is parsed, and its encoding and delimeters are determined.

