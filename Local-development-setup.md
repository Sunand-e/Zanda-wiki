**To set up a fully local deployment of the platform:**

- Clone the API repo. This contains the docker-compose file for container orchestration:

`git clone https://github.com/eLearning-Plus/MemberHub learning-platform-api`

- Enter the `learning-platform-api` directory:

`cd learning-platform-api`

- Create a `.env` file. Pay attention to the `FRONTEND_DIRECTORY` variable

```
# HOST_NAME is used for tenant URLs. For example, if HOST_NAME is set to 'local', the tenant URL will be 'tenant-name.local'.
# You will need a wildcard hosts file entry mapping *.local to 127.0.0.1 for this to work.
# It can also be left blank (Tenant URLs can be individually set in the admin panel).
HOST_NAME=
POSTGRES_USERNAME=pguser
POSTGRES_PASSWORD=pgpass
POSTGRES_DB=learning-platform-db
POSTGRES_HOST=db
# RAILS_MASTER_KEY - is this required? This is currently required, as the rails credentials.yml.enc file contains the 
# jwt_secret_key. This should be moved to the .env file. It also contains the secret_key_base, which is no longer used.
# Once jwt_secret_key is removed, we can stop using the RAILS_MASTER_KEY.
RAILS_MASTER_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
# The `FRONTEND_DIRECTORY` var is used to mount the static files into the nginx container. Nginx serves the files from its own filesystem.
# Ensure this directory exists, and when exporting the frontend, ensure the files are placed in the path given in `FRONTEND_DIRECTORY`.
# The above only applies to the local setup.
FRONTEND_DIRECTORY=~/learning-platform-frontend-export/
FRONTEND_DOMAIN=http://127.0.0.1
RAILS_ENV=development
SMTP_ADDRESS=mailhog
SMTP_PORT=1025
SMTP_DOMAIN=mailhog
MAIL_DEFAULT_FROM_ADDRESS=no-reply@zanda360.com
# AWS_S3_ env vars for uploads to S3:
AWS_S3_BUCKET_ACCESS_KEY_ID=
AWS_S3_BUCKET_SECRET_KEY=
AWS_S3_BUCKET_REGION=eu-west-2
AWS_S3_BUCKET_NAME=
# AWS_CLI_ env vars for use in boto3:
AWS_CLI_ACCESS_KEY_ID=
AWS_CLI_SECRET_KEY=
AWS_DEFAULT_REGION=
REDIS_HOST=redis
# AZURE_CLIENT_ env vars for SSO with Auzre AD:
AZURE_CLIENT_ID=
AZURE_CLIENT_SECRET=
```

As the backend API is secured behind authentication, the easiest way to authenticate with the API is via the frontend.

- In the root directory (the one containing `learning-platform-api` directory), clone the frontend:

`git clone https://github.com/eLearning-Plus/learning-platform-frontend`

- Enter the frontend directory:

`cd learning-platform-frontend`

- Install dependencies:

`npm run install --legacy-peer-deps`
(this works on node v18.12.0, npm v8.19.2, but *should* work on later versions too)

- Build the frontend. This will export the frontend's static files to `/out`:

`npm run build`

- Move the exported files into the FRONTEND_DIRECTORY if necessary:

`learning-platform-frontend-export`

