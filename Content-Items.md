One of the core concepts of the platform, the `ContentItem` model houses multiple types of content - courses, sections, lessons, quizzes, SCORM modules, resources and pathways are all instances of the ContentItem model. All content items are trackable, i.e. for each user, each ContentItem can hold a 'status', and optionally 'progress' and 'score'. The content itself is stored as a JSONB field, 'content', of the ContentItem model.

This documentation outlines the structure and relationships of ContentItems within the platform.

'Assignable' ContentItem Types
-----------------
There are currently three 'assignable' content types - meaning they can be directly assigned to users, or they can be assigned or provided to groups. They are They can also be shared between tenants.

### Courses

These are the core entities at the heart of the platform. Progress for a course is based on the progress values of its children.
    
**Children**:
- **Sections**: Subdivisions of a course. Each section contains one of three types of content, often referred to as "modules" conceptually (though no "Module" class or interface exists in the codebase):

    - **Lesson**: Multimedia educational content, built using a frontend block-based course builder.
            
    - **SCORM Module**: Standardized e-learning package.
            
    - **Quiz**: Assessments to evaluate user knowledge.

### Resources

*   **Description**: Supplementary learning materials that may stand alone or complement courses.
    
        

### 3\. Pathways

*   **Description**: An ordered collection of courses and/or resources.
    
*   **Children**:
    
    *   **Courses**: Integral learning modules.
        
    *   **Resources**: Supporting materials.
        
       

Relationships
-------------

### ContentItemRelationship

Defines hierarchical relationships between ContentItems:

*   **Parent-Child Relationship**: Supports nesting of ContentItems (e.g., Pathway -> Course -> Section -> Lesson).
    

User Interaction
----------------

### UserContentItemRoles

*   **Purpose**: Manages assignments of ContentItems to individual users or groups.
    
*   **Roles**:
    
    *   Assigning ContentItems (Courses, Resources, or Pathways).
        
    *   Monitoring permissions for access and participation.
        

### UserContents

*   **Purpose**: Tracks user-specific data for assigned ContentItems.
       

Tracking and Progress
---------------------

*   **Assignable ContentItems**: All parent ContentItems (Courses, Resources, Pathways) and their components (Sections and module types) are monitored for:
    
    *   **Progress**: How far a user has gone through the content.
        
    *   **Scores**: Achievements in assessments like Quizzes.
        

### Example Use Cases

1.  **Course Assignment**: A Course is assigned to a user. Their progress in sections, lessons, SCORM content, and quizzes is tracked via **UserContents**.
    
2.  **Pathway for Group**: A Pathway containing multiple Courses and Resources is assigned to a group, meaning all users in the group have access to the pathway, and all of its children.
    
3.  **Resource Sharing**: A standalone Resource is assigned to an individual for supplementary learning.