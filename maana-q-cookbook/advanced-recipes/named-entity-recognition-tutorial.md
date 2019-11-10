# Named Entity Recognition Tutorial

This tutorial goes through some sample sequences of events to recognize an entity within a string. For more detailed information about NER's capabilities, go to its [information page](../../product-guide/reference-guide/q-platform-and-microservices/maana-platform-services/named-entity-recognition-ner.md).

**Begin Here:**

Create a new Workspace. Import NER Service \(by searching for service name and dragging to Inventory\) and expand 'Inventory' \(bottom left\)

![Figure 1: Expend &apos;Inventory&apos;: &apos;Services&apos; -&amp;gt; &apos;Maana Named Entity Recognition&apos;](../../.gitbook/assets/image%20%287%29.png)

Then you can drag & drop any service function to you workspace canvas:

#### extract

Drag & drop 'extract' function. On the canvas you'll see new Kind - Extract function Kind.

![Figure 2: Extract function Kind.](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/extractKind.png)

Click on the green function node, then the "run function" button on the right panel \(see Figure 3\).

* Type your text into 'source' field.
* If you have a custom CRF model, drag & drop it into the canvas, then copy its url and paste it into the optional `modelURL` field before checking the box and clicking `Run`

![Figure 3: To extract entities click &apos;RUN&apos; button.](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/source.png)

You will see the results \(extracted entities\) in the bottom section.

![Figure 4: Results of extraction \(click to expand blue triangles\).](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/results1.png)

#### isSurfaceForm

* Drag & drop 'isSurfaceForm' function. On the canvas you'll see new Kind - isSurfaceForm function Kind.
* Click on the function node and then the 'run function' button on the right panel.
* Type your entity in 'source' field.
* Type expected entity name in 'entityName' field \(see all entity names in paragraph "Detected Entities" in this tutorial above\).
* Define 'modelURL' if applicable.
* Click 'RUN' button. See results in the bottom section.

![UpFigure 5: To detect is it surface form click &apos;RUN&apos; button.load](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/isSurfaceForm.png)

\_\_

![Figure 6: Results of if &apos;Microsoft&apos; is surface form of &apos;Organization&apos; type.](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/results2.png)

#### parse

* Drag & drop 'parse' function. On the canvas you'll see new Kind - parse function Kind.
* Click on the function node, then the 'run function' button on the right panel.
* Type your entity in 'source' field.
* Define 'modelURL' if you want to.
* Click 'RUN' button. See results in the bottom section.

\_\_

![Figure 7: To parse entity click &apos;RUN&apos; button.](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/parse.png)

\_\_

![Figure 8: Results of parsing &apos;Forrest Gump&apos; entity.Upload](https://github.com/maana-io/q-tutorials/raw/master/maana-ner-service/results3.png)



