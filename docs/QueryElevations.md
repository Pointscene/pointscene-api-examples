# Interpolate elevation values for GeoJSON LineString feature from surface
GraphQL
```
query{
  interpolateSurfaceElevations(
    surfaceUri:"https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.tif"
    targetResolution:0.5
    distance: 0.1
    feature: {
      type:"Feature"
      properties:{}
      geometry:{
        type:"LineString"
      	coordinates:[[24.908924102783207,60.16625305981004],[24.909916520118717,60.1666987325968]]
      }
    }
  ) {
    geometry{
      type
      coordinates
    }
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "query{interpolateSurfaceElevations(surfaceUri:\"https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.tif\" targetResolution:0.5 distance: 0.1 feature:{type:\"Feature\" properties:{} geometry:{type:\"LineString\" coordinates:[[24.908924102783207,60.16625305981004],[24.909916520118717,60.1666987325968]]}}) {geometry{type coordinates}}}"}' \
https://api.pointscene.com/graphql
```