# Connect Kinds

Let's now upload another file. "mv\_war\_main.csv", once uploaded by dragging and dropping the file onto the Knowledge Graph \(KG\) Canvas, will add an interpreted File Kind onto the Knowledge Graph but renamed to "Drilling Report". 

Select the existing Kind "Well", edit its schema from the Context panel and change the Field type for the "APIWellNumber" field to the Kind "Drilling Report". Save the schema.

This will produce a connection \(blue animated line\) between the two Kinds on the KG based on the primary key APIWellNumber. 

As a user I also expect to be able to easily extend a Field of type Kind \(e.g. "K:foo"\) in an existing Kind \(e.g. "K:bar"\) to a Kind \("K:foo"\) on the Knowledge Graph. In this scenario, the Kind, "K:bar" is connected to the Kind, "K:foo". 

