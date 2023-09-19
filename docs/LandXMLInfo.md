# LandXML info

### This example requires input LandXML as resource (`resourceId`)
### Use resource labels to identify resource later on

GraphQL

```
mutation {
      createWorkflow(
        name:"LandXML workflow"
        instanceId:"{instanceId}"
        tasks:[
 					{
            name:"input"
            type:"resource.input"
            args:{
              id:"{resourceId}"
            }
          }
          {
            name:"info"
            type:"landxml.info"
            inputs:["input"]
            args:{
              epsg:"EPSG:{code}"
            }
          }
          {
            name:"injectMeta"
            type:"resource.injectMeta"
            inputs:["info"]
            args:{
              id:"{resourceId}"
            }
          }
          {
            name:"sync"
            type:"resource.sync"
            args:{
              id:"{resourceId}"
              labels:{
                id:"LandXML-info-resource"
              }
            }
            inputs:["info"]
          }
          {
            name:"enable"
            type:"resource.enable"
            args:{}
            inputs:["sync","injectMeta"]
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
-d '{"query": "mutation{createWorkflow(name:\"LandXML workflow\" instanceId:\"{instanceId}\" tasks:[{name:\"input\" type:\"resource.input\" args:{id:\"{resourceId}\"}}{name:\"info\" type:\"landxml.info\" inputs:[\"input\"] args:{epsg:\"EPSG:{code}\"}}{name:\"injectMeta\" type:\"resource.injectMeta\" inputs:[\"info\"] args:{id:\"{resourceId}\"}}{name:\"sync\"type:\"resource.sync\" args:{id:\"{resourceId}\" labels:{id:\"LandXML-resource\"}} inputs:[\"info\"]}{name:\"enable\" type:\"resource.enable\" args:{} inputs:[\"sync\",\"injectMeta\"]}]){id}}"}' \
https://api.pointscene.com/graphql
```