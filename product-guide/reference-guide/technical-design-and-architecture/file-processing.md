# File Processing

## File Upload

The **Kind:File** represents the **concept** of a file, which includes basic information, such as its name, size, location, etc.  

There are several ways in which files can be ingested:

* **KPortal UI** \(drag-and-drop or file upload dialog\)
* **Maana CLI**
* **Maana Azure Crawler** 

A standard **FileAddedEvent** will be published when the system becomes aware of new files.

![Graylog display of FileAddedEvent](../../../.gitbook/assets/image%20%2865%29.png)

### File Type Detection <a id="FileProcessing-FileTypeDetection"></a>

In response, various **bots inspect** newly discovered files to **harvest** various **metadata**, such as authors, dates and times, formats, encodings, etc.  In order to support an open-ended analysis model, such bots are encouraged to use the following convention in order to promote cooperation across the network:

* A new relation: HasFileMetadata / IsFileMetadataOf
* Links are added of this relation in a strongly typed way: 

```text
{
  fromKind: File,
  fromInstance: 123,
  relationName: HasFileMetadata,
  toKind: MimeType,
  toInstance: text/csv
}
```

As these links are addd, **LinkAdded** events are published and interested listeners for **HasFileMetadata** can perform subsequent processing.

And example of a service that responds to data loading \(via the `hasKindEvent`\) is Field Classifier.

### io.maana.loader <a id="FileProcessing-io.maana.loader"></a>

Maana Q's system loader combines file detection and loading capability in a single **Knowledge Microservice**.  It subscribes to **FileAdded events**, performs a series of **type detection** and **metadata extraction operations**, **recording findings**, and **triggering** the **publication** of **events**.  It also subscribes to these events in order to process the structure and content of the file.

### File Loading <a id="FileProcessing-FileLoading"></a>

When a new file is discovered and its metadata extracted, such as MIME type, it may be appropriate for a **loader bot** to attempt to extract structure and content from the file, such as **records** from an **AVRO-encoded** file, **image** from a **PNG**, or **OCR** from a **PDF**.

### Supported Formats and Extensions 

#### MIME Types 

The following mimetypes are supported: 

* Text extractor: 
  * "application/pdf" 
  * "application/msword" 
  * "application/vnd.openxmlformats-officedocument.presentationml.presentation" 
  * "application/vnd.openxmlformats-officedocument.wordprocessingml.document" 
  * "application/vnd.ms-powerpoint" "application/vnd.ms-excel" 
  * "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
* Image Loader: 
  * "image/png" 
  * "image/jpeg"
* CSV Loader: 
  * "text/csv"
  *  "application/csv"

#### File EXT

If a mimetype is not supplied, the _file extension_ is used to determine how to attempt to load the file. The following file extensions will be handled as follows: 

* Text Extractor:
  *  "pdf"
  *  "doc" "docx" "docm" "dotx"
  *  "xls "xlsm" "xltx" "xltm" "xlsx"
  *  "ppt" "pptx" "pptm" "potx" "potm" "ppsx" "ppsm"
* Image Loader:
  *  "png" "jpeg" "jpg"
* CSV Loader:
  *  "csv"

