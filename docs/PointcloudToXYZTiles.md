# Convert pointcloud to XYZ tiles
## Use labels in `resource.sync` task to identify resource later on
GraphQL
```
mutation {
  createWorkflow(
    name: "pointcloud to xyz tiles"
    instanceId: "{instanceId}"
    tasks: [
      {
        name: "input"
        type: "web.download"
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz"
        }
      }
      {
        name:"tile"
        type:"pdal.tile"
        inputs:["input"]
        args: {
          length:100
          outputFormat:"xyz"
          originX:25504417
          originY:6690976
          writers:{
            text:{
              order:"X,Y,Z,Red,Green,Blue"
              keepUnspecified:false
            }
          }
      	}
      }
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
            id: "point cloud XYZ tiles"
          }
        }
        inputs: ["info"]
      }
      {
        name:"outputTiles"
        type:"resource.upload"
        args:{}
        inputs:["sync","tile"]
      }
      {
        name:"enable"
        type:"resource.enable"
        inputs:["sync","outputTiles"]
      }
    ]
  ) {
    id
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createWorkflow(name:\"pointcloud to xyz tiles\" instanceId: \"{instanceId}\" tasks:[{name:\"input\" type:\"web.download\" args:{url: \"https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz\"}} {name:"\tile\" type:\"pdal.tile\" inputs:[\"input\"] args:{length:100 outputFormat:\"xyz\" originX:25504417 originY:6690976 writers:{text:{order:\"X,Y,Z,Red,Green,Blue\" keepUnspecified:false}}}}{name: \"info\" type: \"pdal.info\" args: {} inputs: [\"input\"]}{name: \"sync\" type: \"resource.sync\" args:{labels:{id: \"point cloud XYZ tiles\"}} inputs: [\"info\"]}{ name:\"outputTiles\" type:\"resource.upload\" args:{} inputs:[\"sync\",\"tile\"]}{name:\"enable\" type:\"resource.enable\" inputs:[\"sync\",\"outputTiles\"]}]){id}}"}' \
https://api.pointscene.com/graphql
```