One of the core concepts of the platform, the `ContentItem` model houses multiple types of content - courses, sections, lessons, quizzes, SCORM modules, resources and pathways are all instances of the ContentItem model. All content items are trackable, i.e. for each user, each ContentItem can hold a 'status', and optionally 'progress' and 'score'. The content item's type is stored in the `item_type` field, and the content itself is stored in the `content` field (JSONB) of the ContentItem model.

This documentation outlines the structure and relationships of ContentItems within the platform.

'Assignable' ContentItem Types
-----------------
There are currently three 'assignable' content types - meaning they can be directly assigned to users, or they can be assigned or provided to groups. They can also be shared between tenants. These types are:

### Courses

These are the core entities at the heart of the platform. Progress for a course is based on the progress values of its children.

### Resources

*   **Description**: Supplementary learning materials that may stand alone or complement courses.

### Pathways

*   **Description**: An ordered collection of courses and/or resources.
       
Content Item Relationships
-------------

The ContentItemRelationship model defines hierarchical relationships between ContentItems, and allows for ordering of content items within their parent.

See [Content Item Relationships](https://github.com/eLearning-Plus/MemberHub/wiki/Content-Item-Relationships) for more details.

User-Content Relationships
----------------

There are two tables that join users to content items: `UserContentItemRoles` and `UserContents`.

### UserContentItemRoles

*   **Purpose**: Manages assignments of ContentItems to individual users or groups.
    
*   **Roles**:
    
    *   Assigning ContentItems (Courses, Resources, or Pathways).
        
    *   Monitoring permissions for access and participation.
        

### UserContents

*   **Purpose**: Tracks user-specific data for assigned ContentItems and their children.
       

Tracking and Progress
---------------------

*   **Assignable ContentItems**: All parent ContentItems (Courses, Resources, Pathways) and their components (Sections and module types) are monitored for:
    
    *   **Progress**: How far a user has gone through the content.
        
    *   **Scores**: Achievements in assessments like Quizzes.
        

### Example Use Cases

1.  **Course Assignment**: A Course is assigned to a user. Their progress in sections, lessons, SCORM content, and quizzes is tracked via **UserContents**.
    
2.  **Pathway for Group**: A Pathway containing multiple Courses and Resources is assigned to a group, meaning all users in the group have access to the pathway, and all of its children.
    
3.  **Resource Sharing**: A standalone Resource is assigned to an individual for supplementary learning.