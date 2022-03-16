# Pointcloud to Surface
## Create surface COG (Cloud Optimized GeoTIFF)
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
          url: "https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.laz"
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