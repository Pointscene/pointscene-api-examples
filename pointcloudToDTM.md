# Pointcloud to DTM
## Create surface COG (Cloud Optimized GEOTiff)
```
mutation {
  createWorkflow(
    name: "pointcloud to surface"
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
        name: "raster"
        type: "pdal.translate"
        inputs:["input"]
        args: {
          filters: [
            {
              range: {
              	limits:"Classification[2:2]"
            	}
            }
            {
              delaunay: {}
            }
            {
              faceraster: {
              	resolution:1
            	}
            }
          ]
          writers: {
            gdal: {
              resolution:1,
              gdaldriver:"GTiff",
              gdalopts: "COMPRESS=LZW,BIGTIFF=YES,TILED=YES",
              dataType: "Float"
            }
          }
        }
      }
      {
        name:"cog"
        type:"gdal.translate"
        inputs:["raster"]
        args: {
          of:"COG"
          co:["COMPRESS=LZW"]
          aSrs:"{EPSGCode}"
        }
      }
    ]
  ) {
    id
  }
}
```