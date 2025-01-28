One of the core concepts of the platform, the `ContentItem` model houses multiple types of content - courses, sections, lessons, quizzes, SCORM modules, resources and pathways are all instances of the ContentItem model. All content items are trackable, i.e. for each user, each ContentItem can hold a 'status', and optionally 'progress' and 'score'. The content item's type is stored in the `item_type` field, and the content itself is stored in the `content` field (JSONB) of the ContentItem model.

This documentation outlines the structure and relationships of ContentItems within the platform.

## 'Assignable' ContentItem Types

There are currently three 'assignable' content types - meaning they can be directly assigned to users, or they can be assigned or provided to groups. They can also be shared between tenants. These types are:

### Courses

These are the core entities at the heart of the platform. Progress for a course is based on the progress values of its children.

### Resources

Supplementary learning materials that may stand alone or complement courses.

### Pathways

An ordered collection of courses and/or resources.

## Content Item Relationships

The ContentItemRelationship model defines hierarchical relationships between ContentItems, and allows for ordering of content items within their parent.

See [Content Item Relationships](https://github.com/eLearning-Plus/MemberHub/wiki/Content-Item-Relationships) for more details.

## User-Content Relationships

There are two models that join users to content items: `UserContentItemRoles` and `UserContents`.

### UserContentItemRoles

`UserContentItemRoles` manages assignments of 'assignable' ContentItems (courses, resources, pathways) to individual users. The role attached to the record determines what actions the user can take for the particular content item.

### UserContents

Tracks user-specific data, e.g. progress, score, and status, for assigned ContentItems and their children.

*   **Progress** - integer from 0 to 100.
*   **Score** - integer from 0 to 100
*   **Completion** - String, one of 'not_started', 'in_progress' or 'completed'. A null value is equivalent to 'not_started'.

When any of the above are updated for a content item, all of it's ancestors are updated too (i.e. a lesson will update its parent section, which will update the parent course. You can see how these are calculated in the `update_ancestor_progress_and_statuses` method of the `UserContent` model.

### Example Use Cases

1.  **Course Assignment**: A Course can be assigned to a user. Their progress in sections, lessons, SCORM content, and quizzes is tracked via **UserContents**.
2.  **Pathway for Group**: A Pathway containing multiple Courses and Resources can be assigned to a group, meaning all users in the group have access to the pathway, and all of its children.
3.  **Resource Sharing**: A standalone Resource can be assigned to an individual for supplementary learning.