# Calculate volume with boundary
```
query{
  surfaceToBoundaryVolume(
    surfaceUri:"https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.tif"
    targetResolution:1
    returnTin:true
    returnTinCrs:"EPSG:3857"
    feature: {
      type:"Feature",
      properties:{},
      geometry:{
        type:"Polygon",
        coordinates:[[[24.910949170589447,60.16728183427011],[24.91146683692932,60.16716708281357],[24.910954535007477,60.16703898769102],[24.91085797548294,60.16717508874213],[24.910949170589447,60.16728183427011]]]
      }
    }
  ) {
    properties
    geometry{
      coordinates
      type
    }
  }
}
```