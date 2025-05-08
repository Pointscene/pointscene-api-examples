# Query scheduled jobs

### Get all jobs
GraphQL
```
query {
  getScheduledJobs(
    instanceId:"{instanceId}"
  ) {
    active
    id
    instanceId
    workflow
    frequencyType
    cronExpression
    intervalMinutes
    nextRun
    lastRun
    createdAt
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query { getScheduledJobs(instanceId: \"{instanceId}\") { active id instanceId workflow frequencyType cronExpression intervalMinutes nextRun lastRun createdAt } }"}' \
https://api.pointscene.com/graphql
```

### Retrieve a specific job with execution history
GraphQL
```
query{
  getScheduledJob(
    jobId:"{jobId}"
  ) {
    id
    instanceId
    history{id jobId success logPath createdAt}
    active
    workflow
    frequencyType
    cronExpression
    intervalMinutes
    nextRun
    lastRun
    createdAt
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query { getScheduledJob(jobId: \"{jobId}\") { id instanceId history{id jobId success logPath createdAt} active workflow frequencyType cronExpression intervalMinutes nextRun lastRun createdAt } }"}' \
https://api.pointscene.com/graphql
```