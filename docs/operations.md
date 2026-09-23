# Operations

## Logs

```bash
aws logs tail /ecs/devops94-idp-svc-reference-api-dev --follow
```

## Current deployment

```bash
aws ecs describe-services --cluster devops94-idp-cluster --services reference-api-dev \
  --query 'services[0].deployments[].{status:status,rollout:rolloutState,taskDefinition:taskDefinition}'
```

## Roll back

Revert the commit on `main` and push; the pipeline redeploys the previous code as a new
immutable image. ECS also rolls back on its own when a new deployment fails health checks
(deployment circuit breaker).

## Pause (cost saving)

Set `desired_count = 0` for the environment in `infra/main.tf` and push.
