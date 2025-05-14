# Delete scheduled job

GraphQL
```
mutation{
  deleteScheduledJob(
    id:"{jobId}"
  ) {
    success
  }
}
```
curl
```
curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {YOUR_AUTH_TOKEN}" \
  -d '{
    "query": "mutation { deleteScheduledJob(id: \"{jobId}\") { success } }"
  }' \
  https://api.pointscene.com/graphql
```