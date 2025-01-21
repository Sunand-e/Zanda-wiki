#### Overview

This development setup leverages **Docker Compose** to orchestrate the application and its associated services. The backend is implemented with Rails, proxied by NGINX for request handling, while the frontend has two modes of operation: production (static export) and development.

#### Backend Services

1.  **Rails Application**:

    -   Runs inside a Docker container.
    -   Processes API requests forwarded by NGINX.
2.  **NGINX**:

    -   Listens on **port 80**.
    -   Serves static frontend files from a local directory, mounted to the container as a volume.
    -   Acts as a reverse proxy, forwarding requests to the Rails application container.

#### Frontend

1.  **Production Mode**:

    -   A statically exported frontend is stored in a local directory.
    -   This directory is mounted as a volume in the Docker Compose configuration to be served by the containers.
2.  **Development Mode**:

    -   Runs on **port 3001** using its own Express server.
    -   The Express server forwards API requests to the backend via NGINX.

#### Volume Mounting

-   Local directories are mounted into containers as volumes to allow seamless development and testing. For instance:
    -   The frontend's static assets are mounted from a specified local directory.
    -   Logs and temporary files are managed using Docker volumes.

See the docker-compose file for more info.

### Setting up a fully local deployment of the platform:

- Clone the API repo. This contains the docker-compose file for container orchestration:

`git clone https://github.com/eLearning-Plus/MemberHub learning-platform-api`

- Enter the `learning-platform-api` directory:

`cd learning-platform-api`

- Create a `.env` file. Pay attention to the `FRONTEND_DIRECTORY` variable

- The **RAILS_MASTER_KEY** is sensitive and is therefore not provided in this documentation. **IT IS CURRENTLY THE SAME RAILS_MASTER_KEY AS IS USED IN PRODUCTION - THIS SHOULD BE CHANGED!**
See: https://stackoverflow.com/questions/60702248/whats-the-correct-way-of-defining-secret-key-base-on-rails-6
and https://blog.saeloun.com/2019/10/10/rails-6-adds-support-for-multi-environment-credentials

```
# HOST_NAME is used for tenant URLs. For example, if HOST_NAME is set to 'local', the tenant URL will be 'tenant-name.local'.
# You will need a wildcard hosts file entry mapping *.local to 127.0.0.1 for this to work.
# It can also be left blank (Tenant URLs can be individually set in the admin panel).
HOST_NAME=
POSTGRES_USERNAME=pguser
POSTGRES_PASSWORD=pgpass
POSTGRES_DB=learning-platform-db
POSTGRES_HOST=db
# RAILS_MASTER_KEY - is this required? YES, as the rails credentials.yml.enc file contains the 
# jwt_secret_key and secret_key_base. These secrets could instead be moved to the .env file, or multi-environment credentials could be used?
RAILS_MASTER_KEY=
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

- Run the containers:

`docker-compose up -d`

- Connect to the rails container:

`docker exec -ti rails bash`

- Seed the database:

`rails db:seed`

- Exit the container:

`exit`

**As the backend API is secured behind authentication, the easiest way to authenticate with the API is via the frontend. You can build the frontend, or use the frontend dev server. The build is faster and more responsive, whereas the dev server will let you see your change to the frontend in real time.**

### Frontend: static export build

- Create a directory to hold the frontend export:

mkdir -p ../learning-platform-frontend-export

- In the root directory (the one containing `learning-platform-api` directory), clone the frontend:

`git clone https://github.com/eLearning-Plus/learning-platform-frontend`

- Enter the frontend directory:

`cd learning-platform-frontend`

- Install dependencies:

`npm run install --legacy-peer-deps`
(this works on node v18.12.0, npm v8.19.2, but *should* work on later versions too)

- Build the frontend. This will export the frontend's static files to `/out`:

`npm run build`

- Move the exported files into the `FRONTEND_DIRECTORY` if necessary:

`mv ./out/* ../learning-platform-frontend-export`

You should now be able to access the frontend at 127.0.0.1:80

### Frontend: development build

- Run the frontend dev server. This will start the next.js dev environment, using a [custom server](https://nextjs.org/docs/pages/building-your-application/configuring/custom-server) located in the frontend repository (`server.js`), which is a basic express server. The reason for the custom server is to allow for redirects for API requests to the rails container running in docker.

`npm run dev`

- The frontend dev environment should be available at: `127.0.0.1:3001`

- The credentials for the 'Super Admin' user account are available in https://github.com/eLearning-Plus/MemberHub/blob/main/db/seeds.rb
