The CI/CD process for deploying the Rails application to Amazon ECS is defined using GitHub Actions and AWS ECS. This process involves building, tagging, and pushing Docker images to Amazon ECR (Elastic Container Registry), updating the ECS task definition, and deploying the updated task definition to the ECS cluster. Notably, this process does not include any testing steps.

#### Workflow Configuration ([deploy-to-aws.yml](https://github.com/eLearning-Plus/MemberHub/blob/sso/.github/workflows/deploy-to-aws.yml))

The GitHub Actions workflow is triggered on push and pull\_request events to the production branch. The workflow consists of several steps:

1.  **Checkout Code**:
    
    *   The workflow uses the actions/checkout@v3 action to check out the code from the repository. This ensures that the latest code changes are available for building the Docker image.
        
2.  **Configure AWS Credentials**:
    
    *   The aws-actions/configure-aws-credentials@v1 action configures AWS credentials using a specified IAM role. This step is necessary for authenticating with AWS services.
        
3.  **Login to Amazon ECR**:
    
    *   The aws-actions/amazon-ecr-login@v1 action logs in to Amazon ECR, allowing the workflow to push Docker images to the registry.
     [View for more details](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws)
        
4.  **Build, Tag, and Push Docker Image**:
    
    *   The workflow builds the Docker image, tags it with latest, and pushes it to Amazon ECR. This step ensures that the latest version of the application is available as a Docker image.
        
5.  **Update ECS Task Definition**:
    
    *   The aws-actions/amazon-ecs-render-task-definition action updates the ECS task definition with the new image. This step modifies the task definition to use the newly built Docker image.
        
6.  **Deploy ECS Task Definition**:
    
    *   The aws-actions/amazon-ecs-deploy-task-definition@v1.4.10 action deploys the updated task definition to the ECS cluster. This step ensures that the ECS service uses the new task definition, effectively deploying the latest version of the application.
        

#### ECS Task Definition ([learning-platform-api-task-definition.json](https://github.com/eLearning-Plus/MemberHub/blob/sso/.aws/learning-platform-api-task-definition.json))

The ECS task definition specifies how the Docker container should be configured and run in the ECS cluster:

1.  **Execution Role**:
    
    *   Specifies the IAM role that ECS uses to pull images and publish logs. This role grants the necessary permissions for these actions.
        
2.  **Container Definitions**:
    
    *   Defines the container configuration, including environment variables, secrets, port mappings, and commands. The container runs the Rails server in production mode and includes necessary environment variables and secrets for the application to function correctly.
        
3.  **Task Role**:
    
    *   Specifies the IAM role that the task can assume, granting it necessary permissions to access AWS resources.
        
4.  **Task Configuration**:
    
    *   Specifies the task family, required compatibilities (EC2 and FARGATE), network mode (awsvpc), CPU, and memory. These settings define the resources and network configuration for the task.
        

### Summary

The CI/CD process involves checking out the code, configuring AWS credentials, logging in to Amazon ECR, building and pushing the Docker image, updating the ECS task definition, and deploying the updated task definition to the ECS cluster. This setup ensures that the application is consistently built and deployed to the production environment. **Notably, the process does not include any testing steps, which means that code changes are deployed directly to production without automated testing.**