# Create indexed pointcloud
## Indexed point cloud and update database
### Use labels in `resource.sync` task to identify output later on
```
mutation {
  createWorkflow(
    name: "Create indexed pointcloud"
    instanceId: "{instanceId}"
    tasks: [
      {
        name: "input",
        type: "web.download",
        args: {
          url: "{pointcloudURL}"
        }
      },
      {
        inputs: ["input"],
        name: "potree",
        type: "potreeconverter.convert",
      },
      {
        name: "info"
        type: "pdal.info"
        args: {}
        inputs: ["input"]
      }
      {
        name: "sync"
        type: "resource.sync"
        args: {
            labels: {
                id: indexed-pointcloud-1
            }
          }
        }
        inputs: ["info"]
      }
      {
        name: "output"
        type: "resource.upload"
        args: {}
        inputs: ["sync", "potree"]
      }
      {
        name: "enable"
        type: "resource.upload"
        args: {}
        inputs: ["sync", "output"]
      }
    ]
  ) {
    id
  }
}
}
```