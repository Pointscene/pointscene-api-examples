# Pointcloud to Potree
## Indexed point cloud and update database
### Use labels in `resource.sync` task to identify output later on
```
mutation {
  createWorkflow(
    name: "Create indexed pointcloud"
    instanceId: "{instanceId}"
    tasks: [
      {
        name: "laz",
        type: "web.download",
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/20191106_Rekolan_urheilupuisto_pistepilvi_final_GK24FIN_N2000.laz"
        }
      },
      {
        inputs: ["laz"],
        name: "potree",
        type: "potreeconverter.convert",
        args: {}
      },
      {
        name: "info"
        type: "pdal.info"
        args: {}
        inputs: ["laz"]
      }
      {
        name: "sync"
        type: "resource.sync"
        args: {
          labels: {
            id:"indexed-pointcloud-1"
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
        type: "resource.enable"
        args: {}
        inputs: ["sync", "output"]
      }
    ]
  ) {
    id
  }
}
```