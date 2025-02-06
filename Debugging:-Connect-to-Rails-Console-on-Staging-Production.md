### Use the following command to connect to the Rails console in the staging environment:

c`luster="learning-platform-staging"`
`service="learning-platform-staging-api-service"`
`container="learning-platform-staging-api"`
`task_id=$(`
  `aws ecs list-tasks \`
    `--cluster $cluster \`
    `--service-name $service \`
    `--desired-status RUNNING \`
    `--output text | awk -F'/' '{print $NF}' | tr '\n' ' ' | awk '{print }'`
`) && \`
`aws ecs execute-command \`
  `--cluster $cluster \`
  `--task $task_id \`
  `--container $container \`
  `--interactive \`
  `--command "/bin/bash"`

Explanation

1. Variables Initialization

cluster="learning-platform-staging"
service="learning-platform-staging-api-service"
container="learning-platform-staging-api"

cluster: ECS cluster where the service is running.

service: The ECS service name for the running API.

container: Target container inside the ECS task.

2. Fetch the Task ID

task_id=$(
  aws ecs list-tasks \
    --cluster $cluster \
    --service-name $service \
    --desired-status RUNNING \
    --output text | awk -F'/' '{print $NF}' | tr '\n' ' ' | awk '{print $1}'
)

aws ecs list-tasks: Lists all running tasks for the specified service.

--desired-status RUNNING: Ensures only running tasks are listed.

awk: Extracts the task ID from the full ARN.

Example ARN:arn:aws:ecs:region:account-id:task/task-idThe task ID is extracted using awk.

3. Execute Command in Container

aws ecs execute-command \
  --cluster $cluster \
  --task $task_id \
  --container $container \
  --interactive \
  --command "/bin/bash"

aws ecs execute-command: Runs a command in the specified container.

--interactive: Keeps the session interactive.

--command "/bin/bash": Launches a bash shell inside the container.

4. Start Rails Console

Once you’re inside the container, start the Rails console:

RAILS_ENV=staging rails c

Replace staging with production if you need to connect to the production environment.

Additional Notes

Ensure AWS CLI is installed and configured.

You need appropriate permissions for aws ecs execute-command.

Replace staging with production if necessary.

