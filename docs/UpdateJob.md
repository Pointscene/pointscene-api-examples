# Update job

GraphQL
```
mutation{
  updateScheduledJob(
    jobId:"{jobId}"
    instanceId:"{instanceId}"
    active:false
  ) {
    id
    active
    lastRun
    nextRun
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation { updateScheduledJob(jobId: \"{jobId}\", instanceId: \"{instanceId}\", active: false) { id active lastRun nextRun } }"}' \
https://api.pointscene.com/graphql
```