# Convert pointcloud to 3D tiles
## Use labels in `resource.sync` task to identify resource later on
GraphQL
```
mutation {
  createWorkflow(
    name: "pointcloud to 3d Tiles"
    instanceId: "{instanceId}"
    tasks: [
      {
        name: "lazInput",
        type: "web.download",
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz"
        }
      }
      {
        name: "geoidInput",
        type: "web.download",
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/FIN2005N00_300m.gtx"
        }
      }
      { 
        type: "convert.resourceToPointcloud"
        name: "laz"
        inputs: ["lazInput"]
      }
      { 
        type: "convert.resourceToGeoid"
        name: "geoid"
        inputs: ["geoidInput"]
      }
      {
        name:"translate"
        type:"pdal.translate"
        inputs:["laz", "geoid"]
        args:{
        	useGeoid:true
          filters: [
            {
              reprojection: {
                inSrs:"+proj=tmerc +lat_0=0 +lon_0=25 +k=1 +x_0=25500000 +y_0=0 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs +geoidgrids=FIN2005N00_300m.gtx"
              	outSrs:"EPSG:3879"
              }
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
        name:"ept"
        type:"entwine21.build"
        args: {
          reprojection:"EPSG:4978"
        }
        inputs:["translate"]
      }
      {
        name:"OGC3DTiles"
        type:"entwine21.convert"
        args: {
          truncate:true
        }
        inputs:["ept"]
      }
      {
        type: "pdal.info"
        name: "info"
        args: {}
        inputs: ["translate"]
      } 
    	{
        name: "sync"
        type: "resource.sync"
        args: {
          labels: {
            id:"3d-tiles-1"
          }
        }
        inputs: ["info"]
      }
      {
        name: "output"
        type: "resource.upload"
        args: {}
        inputs: ["sync", "OGC3DTiles"]
      }
      {
        name: "enable"
        type: "resource.enable"
        inputs: ["sync", "output"]
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
-d '{"query": "mutation {createWorkflow(name:\"pointcloud to 3d Tiles\" instanceId:\"{instanceId}\" tasks:[{name:\"lazInput\" type:\"web.download\" args:{url:\"https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz\"}}{name:\"geoidInput\" type:\"web.download\" args:{url:\"https://storage.googleapis.com/pointscene-sample-data/API-samples/FIN2005N00_300m.gtx\"}}{type:\"convert.resourceToPointcloud\" name:\"laz\" inputs:[\"lazInput\"]}{type:\"convert.resourceToGeoid\" name:\"geoid\" inputs: [\"geoidInput\"]}{name:\"translate\" type:\"pdal.translate\"inputs:[\"laz\", \"geoid\"] args:{useGeoid:true filters: [{reprojection:{inSrs:\"+proj=tmerc +lat_0=0 +lon_0=25 +k=1 +x_0=25500000 +y_0=0 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs +geoidgrids=FIN2005N00_300m.gtx\" outSrs:\"EPSG:3879\"}}] writers:{las:{offsetX:\"auto\" offsetY:\"auto\" offsetZ:\"auto\"}}}}{name:\"ept\" type:\"entwine21.build\" args:{reprojection:\"EPSG:4978\"} inputs:[\"translate\"]}{name:\"OGC3DTiles\" type:\"entwine21.convert\" args:{truncate:true} inputs:[\"ept\"]}{type: \"pdal.info\" name:\"info\" args: {} inputs:[\"translate\"]}{name:\"sync\" type:\"resource.sync\" args:{labels:{id:\"3d-tiles-1\"}} inputs:[\"info\"]}{name:\"output\" type:\"resource.upload\" args:{} inputs: [\"sync\", \"OGC3DTiles\"]}{name:\"enable\" type: \"resource.enable\" inputs: [\"sync\", \"output\"]}]){id}}"}' \
https://api.pointscene.com/graphql
```