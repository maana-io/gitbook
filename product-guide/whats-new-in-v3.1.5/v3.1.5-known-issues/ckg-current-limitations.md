# CKG Current Limitations

## Same kind cannot be used for Input and Output type

* Even with name mangling there are still conflicts as GraphQL schema cannot have same-named Input and Output type
* **Workaround**: create duplicate kind with different name.

## Cannot use kinds from same workspace as input/output of functions

* The issue is that currently KindDB Model boilerplate and CKG schema conflict.
* Manually created workspace is not available as graphQL service CLOSED.
* Real solution requires imports and exports, workspace as a view of a service etc.
* **Workaround**: create workspace with kinds \(i.e. 'model service'\) and use these kinds in workspace with function \('logic service'\).

## Cannot use types that have field named 'id' with type other than 'ID'

* KindDB issue - it requires every kind/type to have field named 'id: ID' or 'id: ID!' and creates it automatically.
* **Workaround**: Until KindDB 2.0 is completed, the workaround is 'EPHEMERAL' field modifier - if the service has no 'id' field, it is added as ephemeral field which is not used in schema generation and query building.

## Type fields with parameters omitted from queries

* There's no such concept as 'arguments' in field, so these will be removed from kind definition on service import.

