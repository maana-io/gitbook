# Curate Extracted Entities

As a user, I want to be able to view the results of the entity extractor bot. Inspecting extracted entities are needed for the following purposes:

* Inspect a high level, summarized view of the results using the appropriate viz
* The ability to click on the relevant Kind and see extracted results in the context of the selected Kind
  * Workspace 1 - running entity extraction on K: text remark produces instances in K: Person, K: Org and K: Location
  * Within workspace 1 or create workspace 2 - running entity extraction on K: text remark\_2 produces additional instances in K: Person, K: Org and K: Location
  * Observe instances in K: Person, K: Org and K: Location filtered based on the source Kind\(s\) selected
* The ability to remove or change labels as needed
* The ability to look at the instances of a Kind and know which ones are sourced from files/documents vs classifier generated

