# Interpolate elevation values for GeoJSON LineString feature
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

Curl sample command:
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2NDc0Mjg2ODYsImV4cCI6MTY0NzQ0MzA4Niwic3ViIjoidXNlci92cVNsIiwianRpIjoiZjQwZDkyZmMtMzc5MC00OTA5LWExZmQtMTlkODI2OTY3ODIxIn0.Gb9ptZ_CptKt20DzRmSR2j9fFqvLta2TNGKXy8AqDF0" \
-d '{"query": "query{interpolateSurfaceElevations(surfaceUri:\"https://storage.googleapis.com/pointscene-sample-data/API-samples/pointcloud_L4133A4.tif\" targetResolution:0.5 distance: 0.1 feature:{type:\"Feature\" properties:{} geometry:{type:\"LineString\" coordinates:[[24.908924102783207,60.16625305981004],[24.909916520118717,60.1666987325968]]}}) {geometry{type coordinates}}}"}' \
https://api.pointscene.com/graphql
```