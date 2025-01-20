### Authentication mechanisms

The [Devise](https://github.com/heartcombo/devise) gem is used to handle user authentication with the following configurations:

- Email-based authentication with case-insensitive and whitespace-stripped email addresses.
- Custom mailer settings using environment variables
- Session storage skipped for HTTP authentication
- CSRF token cleanup on authentication
- Remember me functionality
- Email reconfirmation for email changes
- Password recovery
- Sign out via the DELETE HTTP method
- Invitations, registrations and confirmations
- Integration with Doorkeeper for OAuth 2.0 authentication

Devise config is found at [config/initializers/devise.rb](https://github.com/eLearning-Plus/MemberHub/blob/main/config/initializers/devise.rb)

Devise routes are in [config/routes.rb](https://github.com/eLearning-Plus/MemberHub/blob/main/config/routes.rb)

Devise is implemented for the user model in [app/models/user.rb](https://github.com/eLearning-Plus/MemberHub/blob/main/app/models/user.rb)

JWTs are used for authentication. **THESE ARE CURRENTLY STORED IN LOCALSTORAGE - this should be changed to secure HttpOnly cookies**. an implementation of this has been attempted, alongside Azure ActiveDirectory (EntraID) SSO, in the [sso branch](https://github.com/eLearning-Plus/MemberHub/tree/sso), but it requires further development (namely CSRF-token implementation improvements).