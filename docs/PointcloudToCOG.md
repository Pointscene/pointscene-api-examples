# Convert pointcloud to cloud optimized GeoTIFF
GraphQL
```
mutation{
  createWorkflow(
    instanceId:"{instanceId}"
    name:"Point cloud to COG"
    tasks:[
      {
        name: "input",
        type: "web.download",
        args: {
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz"
        }
      }
      {
        name:"copc"
        type:"pdal.copc"
        inputs:["input"]
        args: {
          softwareId:"pointscene"
          offsetX:"auto"
          offsetY:"auto"
          offsetZ:"auto"
        }
      }
      {
        name:"raster"
        type:"rasterizer.rasterize"
        inputs:["copc"]
        args: {
          epsg:"EPSG:3879"
        }
      }
      {
        name:"cog"
        type:"gdal.translate"
        inputs:["raster"]
        args: {
          of:"COG"
          co:["COMPRESS=LZW"]
        }
      }
    ]
  ) {id}
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createWorkflow(instanceId:\"{instanceId}\" name:\"Point cloud to COG\" tasks:[{name: \"input\" type:\"web.download\" args:{url: \"https://storage.googleapis.com/pointscene-sample-data/API-samples/Rekolan_urheilupuisto_GK25FIN_RGB.laz\"}}{name:\"copc\" type:\"pdal.copc\" inputs:[\"input\"] args: {softwareId:\"pointscene\" offsetX:\"auto\" offsetY:\"auto\" offsetZ:\"auto\"}}{name:\"raster\" type:\"rasterizer.rasterize\" inputs:[\"copc\"] args: {epsg:\"EPSG:3879\"}}{name:\"cog\" type:\"gdal.translate\" inputs:[\"raster\"] args: {of:\"COG\" co:[\"COMPRESS=LZW\"]}}]){id}}"}' \
https://api.pointscene.com/graphql
```