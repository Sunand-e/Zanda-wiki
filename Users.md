Much like any learning platform, the `User` entity is a central concept of the application. 

### Rails model
Represents the users and manages their authentication, profile management, and interactions with other entities. It leverages Devise for authentication and has relationships with tenants, groups, content items, roles, and more. The UserContent model represents the relationship between users and content items, tracking user interactions and progress.

### Users in tenants
- Users only belong to one tenant, including Super Admin. There are mechanisms in place, however, enabling Super Admins to log into ANY tenant.
- Two different tenants can have each a user with the same email address. All users in one tenant must have separate email addresses.
- As the `act_as_paranoid` gem is used on the User model, email addresses for deleted users are prefixed with `deleted_[random_string]_` to allow for users with the same email address as a deleted user to be re-added to the tenant.

### User roles

A user's role(s) determine what actions they can take at the global (tenant) level, at the group level, and at the content level. Ultimately, it is the role system that is responsible for determining if a user has access to a particular content item. Some pre-defined roles are defined in [lib/json_files/roles.json](https://github.com/eLearning-Plus/MemberHub/blob/main/lib/json_files/roles.json). For a more detailed explanation of the role system, see https://sunand-e.github.io/Zanda-wiki/Roles-and-Capabilities

- **Tenant-wide** roles determine what capabilities a user has across the whole tenant. For example, a user can have a 'Tenant Admin' role, and that role has the `CreateCourse` capability.
- **Group-specific** roles determine what capabilities are attached to a user within a particular group - for example, they may have a 'Group Leader' role, which has the `GetUsers` capability. This enables them to see all users who are in the group.
- **Content-level** roles determine the capabilities a user has in relation to a particular content item (course, resource, etc) - these are used to create direct relationships between users and content items, and specify what the user can do with a particular content item.

