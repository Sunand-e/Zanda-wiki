Use the following command to connect to the Rails console in the **staging** environment:

```bash
cluster="learning-platform-staging"
service="learning-platform-staging-api-service"
container="learning-platform-staging-api"
task_id=$(
  aws ecs list-tasks \
    --cluster $cluster \
    --service-name $service \
    --desired-status RUNNING \
    --output text | awk -F'/' '{print $NF}' | tr '\n' ' ' | awk '{print $1}'
) && \
aws ecs execute-command \
  --cluster $cluster \
  --task $task_id \
  --container $container \
  --interactive \
  --command "/bin/bash"
