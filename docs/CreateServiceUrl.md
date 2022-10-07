# Create service URLs for sharing data

## For potree and 3D tiles resources
GraphQL
```
mutation{
  createServiceUrl(
    resourceId:"{resourceId}"
  ) {
   stream
  }
}
```
curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createServiceUrl(resourceId:\"{resourceId}\"){stream}}"}' \
https://api.pointscene.com/graphql
```

## TMS, XYZ, WMS and WMTS for ortho COG resource
GraphQL
```
mutation{
  createServiceUrl(
    resourceId:"{resourceId}"
    objectName:"ortho-cog.tif"
  ) {
   tms
   xyz
   wms
   wmts
  }
}
```

curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createServiceUrl(resourceId:\"{resourceId}\" objectName:\"ortho-cog.tif\"){tms xyz wms wmts}}"}' \
https://api.pointscene.com/graphql
```