LMS Group & Organisation Management Documentation
-------------------------------------------------

### 1\. Overview

This document details the functionalities related to Groups and Organisations within the LMS, including credits-based user management, permissions, and content assignment. It covers:

-   Group-based course provisioning and enrolments

-   Credits system for organisations

-   Roles and permissions for Group Leaders, Organisation Leaders, and Tenant Admins

-   Capabilities related to content assignment (EnrolUsersInContent)

-   Credit distribution and tracking for training resellers

### 2\. Groups & Organisations

#### 2.1. Groups

A group represents a business client that has:

-   A set of courses assigned via `GroupContent` or `GroupProvisionedCourses`.

-   One or more Group Leaders responsible for user enrolments and reports.

#### 2.2. Organisations (Special Type of Group)

Organisations are structured as groups but with additional constraints:

-   Organisations exclusively use the **credits system** for course enrolments.

-   Organisation Leaders can only manage one organisation.

-   Any user created by an Organisation Leader is automatically assigned to the same organisation.

-   Organisation Leaders can:

    -   Upload new users (restricted to their own organisation).

    -   Assign only `GroupProvisionedCourses` to users.

    -   View reports for their organisation.

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

-   View reports on user progress.

##### 4.1.1. Restrictions

-   A Group Leader does not use the credits system.

-   They can only assign users the `Member` role.

-   If an enrolment action exceeds available licenses, it is blocked.

#### 4.2. Organisation Leader

An Organisation Leader has similar responsibilities to a Group Leader but with additional constraints:

-   They can **only upload new users to their own organisation**.

-   They can **only assign GroupProvisionedCourses**.

-   They can **see reports related to their organisation**.

-   They can **only delete users they initially created**, provided those users are not in another group.

-   **They cannot remove Group Leaders.**

-   **They have visibility into the remaining credits before assigning courses.**

#### 4.3. Tenant Admin

A Tenant Admin oversees multiple organisations and manages credits. They can:

-   View the current credit count and total credits for each organisation.

-   Increase an organisation's total credits (`credits_increment`).

-   Designate a group as an organisation (`is_organisation` flag).

-   Ensure that Organisation Leaders only assign the `Member` role to users.

-   Track credit distribution to organisations.

### 5\. System Constraints & Checks

| Check | Condition | Action |
| Course Assignment Limit | If total assigned courses exceed available credits | Block assignment. |
| Bulk Enrolments | If bulk action exceeds available credits | Block entire action. |
| User Deletion | If user belongs to multiple groups | Block deletion. |
| User Role Assignment | Group Leaders can only assign the `Member` role | Enforce restriction. |
| Organisation Leader Removal | Attempt to remove a Group Leader | Block action. |
| Credit Distribution Reporting | Total credits distributed per tenant | Log and report data. |

### 6\. Key Takeaways

-   Only **organisations** use the **credits system** to control course assignments.

-   **One credit = One course per user.**

-   Tenant Admins allocate credits; Organisation Leaders assign courses within credit limits.

-   **Organisation Leaders cannot remove Group Leaders.**

-   Course assignment actions fail if they exceed available credits.

-   **Credit distribution and tracking are logged for resellers.**