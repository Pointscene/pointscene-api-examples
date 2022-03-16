# Creating service URLs for sharing data

## For potree resource
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
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createServiceUrl(resourceId:\"{resourceId}\"){stream}}"}' \
https://api.pointscene.com/graphql
```

## WMTS for ortho COG 
GraphQL
```
mutation{
  createServiceUrl(
    resourceId:"{resourceId}"
    objectName:"ortho-cog.tif"
  ) {
   wmts
  }
}
```

curl
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createServiceUrl(resourceId:\"{resourceId}\" objectName:\"ortho-cog.tif\"){wmts}}"}' \
https://api.pointscene.com/graphql
```