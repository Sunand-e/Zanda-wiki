Groups and Organisations

### Multi-Tenant Structure: Groups and Organisations

In the platform, **tenants** either use **groups** or **organisations**, depending on whether they are resellers or not. The key difference lies in how these groups or organisations manage users and enrolments. A tenant can have multiple groups or organisations within it. They could even have both, but extra attention must be given to the UI for this to be a solid offering.

*   **Tenant**: The primary unit in your multi-tenant system. Each tenant represents a separate business or entity. A tenant can have multiple **groups** or **organisations** within it.
*   **Group** (Non-Reseller Clients):
    *   **Purpose**: Groups are used for non-reseller clients who simply need to assign courses to users without managing enrolment limits or credits.
    *   **No Enrolment Limits**: There are no restrictions on how many users can be added to a group, and no tracking of enrolment credits.
*   **Organisation** (Resellers):
    *   **Purpose**: Organisations are a special type of group designed for resellers. They come with the ability to manage **enrolment licences**, which restrict how many users can be enrolled based on available credits.
    *   **Enrolment Management**: Organisations are provided with a set of enrolment licenses. Each license corresponds to one user being able to enrol in a course, and these licences are consumed as users are added and assigned courses.

### Tenant Admin Role in Managing Groups and Organisations

The **tenant admin** plays a central role in managing both groups and organisations within the tenant:

1.  **Managing Groups and Organisations**:
    *   The tenant admin can create either standard **groups** (for non-reseller clients) or **organisations** (for resellers).
    *   For organisations, the admin has the ability to set and adjust the number of enrolment licences available (the total number of users that can be enrolled in courses under that organisation).
2.  **Enrolment License Management**:
    *   Tenant admins have oversight over how many enrolment licences an organisation has and can increase this number as necessary.
    *   They can monitor enrolment usage across both groups and organisations, ensuring that no organisation exceeds its licence quota.

### Key Functional Differences

*   **Groups**:
    *   Groups do not have an enrolment limit and are typically used by non-reseller clients. They can assign as many users to courses as needed without concern for enrolment credits.
*   **Organisations**:
    *   Organisations are designed for resellers and come with additional functionality around **enrolment credits**. Each enrolment license corresponds to a user that can be enrolled in any course, and organisations are restricted by the number of credits available to them.
    *   The system ensures that users can only be added to organisations up to the limit of available credits. Once the enrolment credits are exhausted, no more users can be added unless additional credits are granted.

### Conditional Workflow

*   **Standard Group**: Users can be added and courses can be assigned freely without restrictions on enrolment licences.
*   **Organisation**: The system checks available enrolment credits before allowing a new user to be added to the organisation. If there are no credits left, no additional users can be added or enrolled in courses.

This setup ensures that resellers can manage their users and enrolments within the limits of their credits, while non-reseller clients have the flexibility to assign courses to any number of users within their group.

### Summary

In your platform, **groups** are for regular clients who don’t need enrolment limits, and **organisations** are for resellers who need to manage enrolment licences. The tenant admin is responsible for overseeing both types of groups, managing enrolment credits for organisations, and ensuring the system functions within the boundaries of those credits. This structure offers flexibility for both types of clients, supporting the needs of resellers while simplifying user management for standard clients.