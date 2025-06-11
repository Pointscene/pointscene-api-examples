# Query scheduled jobs

### Get all jobs with lates execution history
GraphQL
```
query {
  getScheduledJobs(
    instanceId:"{instanceId}"
  ) {
    active
    id
    history{id jobId success logPath createdAt}
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

### Retrieve a specific job with latest execution history
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

### Retrieve execution history for all jobs  

GraphQL - basic query (first page)
```
query {
  getInstanceJobHistory(
    instanceId: "{instanceId}"
    page: {
      first: 20
    }
  ) {
    items {
      id
      jobId
      success
      logPath
      createdAt
    }
    cursor
    hasNextPage
  }
}
```

curl
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query { getInstanceJobHistory(instanceId: \"{instanceId}\", page: { first: 20 }) { items { id jobId success logPath createdAt } cursor hasNextPage } }"}' \
https://api.pointscene.com/graphql
```
GraphQL - Fetching Subsequent Pages
```
query {
  getInstanceJobHistory(
    instanceId: "{instanceId}"
    page: {
      first: 20
      after: "{cursor_from_previous_response}"
    }
  ) {
    items {
      id
      jobId
      success
      logPath
      createdAt
    }
    cursor
    hasNextPage
  }
}
```

curl
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query { getInstanceJobHistory(instanceId: \"{instanceId}\", page: { first: 20, after: \"{cursor_from_previous_response}\" }) { items { id jobId success logPath createdAt } cursor hasNextPage } }"}' \
https://api.pointscene.com/graphql
```

### Retrieve execution history by history id  

GraphQL

```
query{
  getScheduledJobHistory(
    jobHistoryId:"{jobHistoryId}"
  ) {
    id jobId success createdAt signedLogUrl
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query { getScheduledJobHistory(jobHistoryId: \"{jobHistoryId}\") { id jobId success createdAt signedLogUrl } }"}' \
https://api.pointscene.com/graphql
```