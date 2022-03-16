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
        name: "input"
        type: "web.download"
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.laz"
        }
      }
      {
        name:"filter"
        type:"pdal.translate"
        inputs:["input"]
        args: {
          filters: [
            {
              voxeldownsize: {}
            }
        	]
          writers: {
            las: {
              offsetX:"auto"
              offsetY:"auto"
              offsetZ:"auto"
            }
          }
      	}
      }
      {
        inputs: ["filter"]
        name: "potree"
        type: "potreeconverter.convert"
        args: {
          outputFormat:"LAS"
        }
      }
      {
        name: "info"
        type: "pdal.info"
        args: {}
        inputs: ["filter"]
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

Curl sample command:
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJh..." \
-d '{"query": "mutation{createWorkflow(name:\"Create indexed pointcloud\" instanceId: \"{instanceId}\" tasks:[{name:\"input\" type:\"web.download\" args:{url:\"https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.laz\"}} {name:\"filter\" type:\"pdal.translate\" inputs:[\"input\"] args:{filters:[{voxeldownsize:{}}] writers:{las:{offsetX:\"auto\" offsetY:\"auto\" offsetZ:\"auto\"}}}}{inputs:[\"filter\"] name:\"potree\" type:\"potreeconverter.convert\" args:{outputFormat:\"LAS\"}}{name:\"info\" type:\"pdal.info\" args:{} inputs:[\"filter\"]}{name:\"sync\" type:\"resource.sync\" args:{labels:{id:\"indexed-pointcloud-1\"}} inputs:[\"info\"]}{name:\"output\" type:\"resource.upload\" args:{} inputs:[\"sync\", \"potree\"]}{name:\"enable\" type:\"resource.enable\" args:{} inputs:[\"sync\",\"output\"]}]){id}}"}' \
https://api.pointscene.com/graphql
```