The [Devise](https://github.com/heartcombo/devise) gem is used for authentication.

The Devise config is found at: https://github.com/eLearning-Plus/MemberHub/blob/main/config/initializers/devise.rb

Devise is being used to handle user authentication with the following configurations:

- Email-based authentication with case-insensitive and whitespace-stripped email addresses.
- Custom mailer settings using environment variables.
- ActiveRecord as the ORM.
- Session storage skipped for HTTP authentication.
- CSRF token cleanup on authentication.
- Password hashing with a configurable cost factor and length validation.
- Remember me functionality with token invalidation on sign out.
- Email reconfirmation for email changes.
- Password recovery with a specified time interval.
- Scoped views for Devise.
- Sign out via the DELETE HTTP method.

Devise is being used in the [User model](https://github.com/eLearning-Plus/MemberHub/blob/main/app/models/user.rb) to handle various aspects of user authentication and management, including:

Email-based authentication
User registration and account management
Email confirmation
Password recovery
Remember me functionality
Tracking user sign-ins
Inviting users to the application
Integrating with Doorkeeper for OAuth 2.0 authentication
These features provide a comprehensive authentication solution for managing users within the application.