# Create scheduled synchronization job

GraphQL
```
mutation {
  createScheduledJob(
    instanceId: "{instanceId}"
    workflow: {
      name: "Sync job"
      instanceId: "{instanceId}"
      tasks: [
        {
          name:"sync"
          type:"sync.files"
          inputs:[]
          args:{
            resourceId:"{resourceId}"
            remotes:[
              "acc:/Project Files"
              "drive:/workdata"
            ]
          }
        }
      ]
    }
    frequencyType: CRON_BASED
    cronExpression: "0 6 * * *"
    active: true
    name:"ACC and Google Drive sync"
    description:"Automated daily synchronization between Autodesk Construction Cloud and Google Drive at 6:00 AM."
  ) {
    id
    instanceId
    workflow
    frequencyType
    cronExpression
    intervalMinutes
    nextRun
    lastRun
  }
}
```
curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation { createScheduledJob(instanceId: \"{instanceId}\", workflow: {name: \"Sync job\", instanceId: \"{instanceId}\", tasks: [{name:\"input\", type:\"resource.input\", args:{id:\"{resourceId}\", exclude:[\"sync/**\", \".log/**\"]}}, {name:\"syncTask\", type:\"rclone.sync\", args:{id:\"{resourceId}\", remotes:[\"acc:/Project Files\", \"drive:/workdata\"]}, inputs:\"input\"}]}, frequencyType: CRON_BASED, cronExpression: \"0 6 * * *\", active: true, name:\"ACC and Google Drive sync\", description:\"Automated daily synchronization between Autodesk Construction Cloud and Google Drive at 6:00 AM.\") { id instanceId workflow frequencyType cronExpression intervalMinutes nextRun lastRun } }"}' \
https://api.pointscene.com/graphql
```