### 1\. Overview

This document details the functionalities related to Groups and Organisations within the LMS, including credits-based user management, permissions, and content assignment. It covers:

-   Group-based course provisioning and enrolments

-   Credits system for organisations

-   Roles and permissions for Group Leaders and Tenant Admins

-   Capabilities related to content assignment (EnrolUsersInContent)

-   Credit distribution and tracking for training resellers

### 2\. Groups & Organisations

#### 2.1. Groups

A group represents a business client that has:

-   **Assigned Content**: All members of the group (or users with any other role in GroupMemberships model) gain access to the content.

-   **Provisioned Content:** The Group Leader can directly assign any group provisioned content to any members within the group.

-   **Group Leaders** can report on their group courses and users

-   Any user created by a Group Leader is automatically assigned to the same group.

#### 2.2. Organisations (Special Type of Group)

Organisations are structured as groups but with additional features:

-   boolean property `isOrganisation` of the group is set to `true` 

-   Organisations exclusively use the **credits system** for course enrolments.

-   A user with a **Group Leader** role in an organisation is referred to as an '**Organisation Leader**'.

-   Organisation Leaders can:

    -   Upload new users (restricted to their own organisation).

    -   Edit user details and remove users (with constraints, but **cannot remove Group Leaders**).

    -   Users removed from an organisation cannot be part of another group.

    -   See an indicator of 'remaining credits' when assigning users to courses.

### 3\. Credits System for Organisations

#### 3.1. Overview of the Credits System

Organisations use a credits-based system for course enrolment. Each organisation is allocated a number of credits, which determine the number of courses users can be enrolled in.

-   **One credit = One course assigned to one user.**

-   If all credits are used, new course assignments are blocked.

-   Organisation Leaders cannot assign more courses than available credits.

-   Tenant Admins can increase the credit count.

-   Training resellers can distribute credits to organisations and track how many they have distributed.

#### 3.2. Credit System Scenarios

**Example Scenario:**

-   A Tenant Admin creates an organisation and allocates 10 credits.

-   The organisation is provided with access to 20 courses.

-   The Organisation Leader attempts to assign 20 courses to a single user (this should fail because only 10 credits are available).

-   The Organisation Leader attempts to assign 10 courses to three users (this should fail because 30 credits would be required, but only 10 are available).

#### 3.3. Credit Attributes

| Attribute | Description |
| `credits_total` | Total number of credits allocated to the organisation. |
| `credits_used` | Number of credits currently consumed. |
|  |  |

#### 3.4. Credit Transactions & Reporting

-   Each transaction of credits (credits given to an organisation) is logged with a date and number of credits.

-   **Transaction Table Columns:**

    -   `tenantId`

    -   `groupId`

    -   `creditCount`

-   The total number of credits distributed to a tenant's organisations can be retrieved by selecting from the transaction table grouped by `tenant_id`.

-   Resellers need visibility into `elp credits used` / `elp credit total` for each organisation.

-   Reports on credit usage per content item can be retrieved from `TenantContentItem.credits_used`.

#### 3.5. Credit Enforcement

-   If an Organisation Leader tries to assign a course and no credits are available, the action is blocked.

-   Bulk enrolments (`EnrolUsersInContent`) are blocked if they exceed available credits.

-   Tenant Admins can increase the `credits_total` to allow more course assignments.

-   Restrict credit functionality to just courses in `EnrolUsersInContent` mutation.

### 4\. Roles & Permissions

#### 4.1. Group Leader

A Group Leader manages users and enrolments within a group. They can:

-   Assign courses from `GroupContent` to users.

-   Create new users in their group.

-   View reports on user progress

-   They can only upload new users to their own group (they will be added as group 'members').

**4.2. Tenant Admin**

A Tenant Admin oversees multiple groups / organisations and manages credits for organisations. They can:

-   Add users to a group as eithe r a member or a group leader

-   View the current credit count and total credits for each organisation.

-   Increase an organisation's total credits (`credits_increment`).

-   Designate a group as an organisation (`is_organisation` flag).

-   Ensure that Organisation Leaders only assign the `Member` role to users.

-   Track credit distribution to organisations.

### 5\. System Constraints & Checks

These should be checked as a Group Leader / Org Leader so we can be sure Groups are working as expected:

| Check | Condition | Action |
| Course Assignment Limit | If total assigned courses exceed available credits for organisation | Block assignment. |
| Bulk Assignments | If bulk action exceeds available credits | Block entire action. |
| User Deletion | If user belongs to multiple groups | Block deletion. |
| User Creation | User should be added as member to the Group Leader's group | Create additional GroupMembership entry. |
| Organisation Leader Removal | Attempt to remove a Group Leader | Block action. |
|  |