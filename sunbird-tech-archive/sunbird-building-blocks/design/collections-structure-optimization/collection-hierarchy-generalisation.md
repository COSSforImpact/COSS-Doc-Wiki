---
icon: elementor
---

# Collection Hierarchy Generalisation

### Overview: <a href="#collectionhierarchygeneralisation-overview" id="collectionhierarchygeneralisation-overview"></a>

Collection hierarchy structure should support different type of objects as children.

### Current Behaviour: <a href="#collectionhierarchygeneralisation-currentbehaviour" id="collectionhierarchygeneralisation-currentbehaviour"></a>

* A Collection hierarchy supports Content with visibility Default and Collection with visibility as Parent and Default as children.
* Child Collection with visibility Parent can be edited but child Collection and Content with visibility Default can not be modified as part of hierarchy modification.

### ![](https://imgr.whimsical.com/object/3mCzefopkUi6LBU6YTN7cH) <a href="#collectionhierarchygeneralisation" id="collectionhierarchygeneralisation"></a>

### Expected Behaviour: <a href="#collectionhierarchygeneralisation-expectedbehaviour" id="collectionhierarchygeneralisation-expectedbehaviour"></a>

* A Collection hierarchy should support multiple objects as children.
* Currently Collection Hierarchy should support Question and QuestionSet with visibility Default as children.

![](https://imgr.whimsical.com/object/Rd6mFbiptFS1SzNvu7gFog)

**Open Question:**

1. Whether there should be any configured list of objectType which will be supported as children in Collection hierarchy?
2. Question and QuestionSet object type should be supported?
3. ChildNodes will have all the leafNodes ? What about Question and QuestionSet?

### Implementation Design Approach: <a href="#collectionhierarchygeneralisation-implementationdesignapproach" id="collectionhierarchygeneralisation-implementationdesignapproach"></a>

* Collection hierarchy will have support for multiple objects as children.
* Child objectType will be validated from configuration list.
* Currently Collection hierarchy will support Question and QuestionSet of visibility as Default as children.
* It means child Question and QuestionSet will not be updated and published in Collection API work flow.

**Update Hierarchy:**

* As part of hierarchy update API, multiple type of object (Question and QuestionSet) will be added into collection hierarchy.
* Different types of object (Question and QuestionsSet) with visibility as Default can be passed in children list of root collection or unit collection in hierarchy.
* There is no support for child objects with visibility Parent in collection hierarchy - except Collection object.
* Status of the child objects will not be validated as part of hierarchy update.
* Index, Depth and Parent will be set for Question and Question Set

**Read Hierarchy:**

* With mode=edit
  * Hierarchy will be fetched from Cassandra table.
* Without mode=edit
  * Unpublished version of hierarchy will be fetched.
  * Similar to child Content and Collection with visibility Default, current updated version of child objects (Question and QuestionSet) with visibility Default will be fetched and metadata will be set in hierarchy.

**Add LeafNode:**

* Similar to child Content and Collection with visibility as Default, other child object (Question and QuestionSet) with visibility as Default can be passed in children list to be linked as children with root or unit collection accordingly.
* Objects will be linked to respective root or unit collection at the end of current index.

**Remove LeafNode:**

* Similar to child Content and Collection with visibility as Default, other child object (Question and QuestionSet) with visibility as Default can be passed in children list to be removed from root or unit collection children accordingly.
* Objects will be delinked from respective root or unit collection and index will be recalculated accordingly.

**Collection Publish:**

* While enriching children metadata in collection hierarchy, data will be fetched form Neo4j or Cassandra hierarchy table - based on object type.
  * Currently it is getting handled based on mimeType
  * Enrich child QuestionSet with visibility as Default - the way child Collection with visibility as Default gets enriched.
  * Enrich child Question with visibility as Default - the way child Content with visibility as Default gets enriched.
* ChildNodes list will be updated wit all leaf nodes (depends upon objectType). (It is a open Question - 3)
* Calculate leafeNodeCount, mimeTypeCount and contentTypeCount calculation - based on objectType. (It is a open Question - 3)
* Link child leafNodes with root collection as Neo4j relationship - depends upon objectType. (It is a open Question - 3)
* Handle different child objects (Question and QuestionSet) while generation of Ecar.
