# 04: Connect Kinds

\[TBD\]

Upload another file, "mv\_war\_main.csv", add its interpreted Kind on to the KG and rename to "Drilling Report". 

Select the existing Kind "Well", edit its schema from the Context panel and change the Field type for the "APIWellNumber" field to the Kind "Drilling Report". Save the schema.

This will produce a connection \(blue animated line\) between the two Kinds on the KG based on the primary key APIWellNumber. 

As a user I also expect to be able to easily extend out a Field of type Kind \(say K:foo\) in an existing Kind \(say K:bar\) to that Kind \(K:foo\) on the KG. In this scenario, the Kind, K:bar is connected to the Kind, K:foo. 

