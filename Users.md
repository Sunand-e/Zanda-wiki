Much like any learning platform, the `User` entity is a central concept of the application. 

### Rails model
Represents the users and manages their authentication, profile management, and interactions with other entities. It leverages Devise for authentication and has relationships with tenants, groups, content items, roles, and more. The UserContent model represents the relationship between users and content items, tracking user interactions and progress.

### Users in tenants
- Users only belong to one tenant, including Super Admin. There are mechanisms in place, however, enabling Super Admins to log into ANY tenant.
- Two different tenants can have each a user with the same email address. All users in one tenant must have separate email addresses.
- As the `act_as_paranoid` gem is used on the User model, email addresses for deleted users are prefixed with `deleted_[random_string]_` to allow for users with the same email address as a deleted user to be re-added to the tenant.

### User roles
**Roles and Permissions**:

*   Pre-set roles are defined in a JSON file and stored in the database.    
*   Global roles include Tenant Admin, Supervisor, and Learner.    
*   Group-specific roles such as Group Leader and Member.    
*   Content-level roles like Learner or Editor (customizable).    
*   Role capabilities managed via a many-to-many relationship with the roles\_capabilities table.

