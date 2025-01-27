The relationships between content items are defined in the ContentItemRelationship model, allowing for hierarchical relationships between ContentItems, and ordering of items within a parent. The columns of the `content_item_relationships` table in the db are `id`, `content_item_id`, `parent_id` and `order`.

### Relationship rules

The current rules for the relationships are as follows:

**Pathways** may only have **courses** or **resources** as children. Pathways do not have parent content items.

**Courses** may only have **sections** as their children, and may belong to multiple **pathways**.

**Sections** may only have **lessons**, **SCORM modules**, or **quizzes** as their children. Sections must only belong to one **course**.

**Lessons**, **SCORM modules**, and **quizzes** do not have child content items, and may only belong to one **section**.

**Resources** do not have child content items, but may belong to multiple **pathways**.

### Ordering

The ‘order’ field of a content item relationship determines the order of the child content item within its parent content item.