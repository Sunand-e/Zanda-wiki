The staging and production environments for Zanda 360 are hosted on Amazon Web Services.

Here is an outline of the services used in production, and a brief overview of how each service is used.

## Amazon ECS

### Task Definitions

Two ECS task definitions are defined; one for the API service, and one for the frontend service.

#### Frontend Task Definition:

- Uses an image based on nginx, which is built by the frontend CI/CD workflow.
- Serves as the entrypoint for all requests to the platform.
- Configured to run on Fargate with specific CPU and memory allocations.
- Defines container port mappings for HTTP traffic.

See: [learning-platform-nginx-task-definition.json](https://github.com/eLearning-Plus/learning-platform-frontend/blob/main/.aws/learning-platform-nginx-task-definition.json) for more details 

#### API Task Definition:

- Uses the busybox:latest image.
- Configured to run on Fargate with specific CPU and memory allocations.
- Defines container port mappings for a simple HTTP server.

### ECS Services

Two ECS services are defined: one for the frontend/nginx task, and one for the backend api task. The nginx task is associated with a target group, meaning that for any tasks registered in the service, AWS will dynamically register the IP to target group.

### ECS Cluster

Both services reside within the production cluster, `learning-platform-cluster1`

## Load balancer - ALB

There is one load balancer for both the staging and production environments - certificates are attached for the following domains:
- *.staging.zanda360.com

- *.zanda360.com
- *.staging.smartlms.co.uk
- *.smartlms.co.uk

The load balancer forwards to the target group associated with the ECS nginx service.

## RDS
A multi-AZ PostgreSQL instance is used as the database which the rails API ECS task has access to.

## Parameter Store

AWS Systems Manager's **Parameter Store** is used to securely store various secrets for the platform:
- **HOST_NAME**: The hostname of the application.
- **MAIL_DEFAULT_FROM_ADDRESS**: The default email address used for sending emails.
- **POSTGRES_DB**: The name of the PostgreSQL database.
- **POSTGRES_HOST**: The hostname or IP address of the PostgreSQL server.
- **POSTGRES_PASSWORD**: The password for the PostgreSQL user.
- **POSTGRES_USERNAME**: The username for the PostgreSQL database.
- **RAILS_MASTER_KEY**: The master key for Rails encrypted credentials.
- **REDIS_HOST**: The hostname or IP address of the Redis server.
- **S3_BUCKET_ACCESS_KEY_ID**: The access key ID for the S3 bucket.
- **S3_BUCKET_NAME**: The name of the S3 bucket.
- **S3_BUCKET_REGION**: The region where the S3 bucket is located.
- **S3_BUCKET_SECRET_KEY**: The secret access key for the S3 bucket.
- **SMTP_ADDRESS**: The address of the SMTP server.
- **SMTP_DOMAIN**: The domain used by the SMTP server.
- **SMTP_USERNAME**: The username for the SMTP server.
- **SMTP_PASSWORD**: The password for the SMTP server.
- **SMTP_PORT**: The port used by the SMTP server.
