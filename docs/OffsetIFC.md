# IFC offset

## Offset IFC file to be used in Pointscene.js
### Requires input IFC as resource (`resourceId`) and empty resource for output (`outputResourceId`)
### Use resource labels to identify resource later on

GraphQL

```
mutation {
      createWorkflow(
        name:"IFC offset workflow"
        instanceId:"{instanceId}"
        tasks: [
          {
            name:"input"
            type:"resource.input"
            args:{
              id: "{resourceId}"
            }
          }
          {
            name:"offset",
            type:"ifc.offset"
            inputs:["input"]
          }
          {
            name:"inputInfo"
            type:"ifc.info"
            args: {
              epsg:"EPSG:{code}"
            }
            inputs:["input"]
          }
          {
            name:"injectMetaOutput"
            type:"resource.injectMeta"
            inputs:["inputInfo","offset"]
            args:{
              id:"{outputResourceId}"
            }
          }
          {
            name:"syncOutput"
            type:"resource.sync"
            args: {
              id:"{outputResourceId}"
              labels: {
                id:"offsetted-ifc"
              }
            }
            inputs:["inputInfo"]
          }
          {
            name:"output"
            type:"resource.upload"
            args:{}
            inputs:["syncOutput","offset"]
          }
          {
            name:"enableOutput"
            type:"resource.enable"
            args:{}
            inputs:["syncOutput","output","injectMetaOutput"]
          }
        ]
      ) { id }
    }
```

curl

```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createWorkflow(name:\"IFC offset workflow\" instanceId:\"{instanceId}\" tasks:[{name:\"input\" type:\"resource.input\" args:{id:\"{resourceId}\"}}{name:\"offset\"  type:\"ifc.offset\" inputs:[\"input\"]}{name:\"inputInfo\" type:\"ifc.info\" args:{epsg:\"EPSG:{code}\"} inputs:[\"input\"]}{name:\"injectMetaOutput\" type:\"resource.injectMeta\" inputs:[\"inputInfo\",\"offset\"] args:{id:\"{outputResourceId}\"}}{name:\"syncOutput\" type:\"resource.sync\" args:{id:\"{outputResourceId}\" labels:{id:\"offsetted-ifc\"}} inputs:[\"inputInfo\"]}{name:\"output\" type:\"resource.upload\" args:{} inputs:[\"syncOutput\",\"offset\"]}{name:\"enableOutput\" type:\"resource.enable\" args:{} inputs:[\"syncOutput\",\"output\",\"injectMetaOutput\"]}]) { id }}"}' \
https://api.pointscene.com/graphql
```