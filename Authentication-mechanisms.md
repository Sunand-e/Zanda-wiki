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

Devise config is found at: [config/initializers/devise.rb](https://github.com/eLearning-Plus/MemberHub/blob/main/config/initializers/devise.rb)
Devise routes are in routes.rb

### New User flow

The common way in which users are set up on the platform for each new client is that the Super Admin creates a new tenant, and creates a new user with the global 'Tenant Admin' role for the client admin's email address. The tenant admin then imports users via a CSV (or adds them manually). Each user is assigned the global 'Learner' role. During or after user creation, the users can be sent an 'invitation'. Currently, public sign-up is not used, and so currently, the email confirmation is currently skipped.

Note - Each CSV import is stored using the `BulkImport` and `BulkImportUser` models. These `BulkImport`s are currently unused.