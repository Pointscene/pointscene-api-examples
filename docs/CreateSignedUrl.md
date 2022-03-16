# Create signed URL
GraphQL
```
mutation{
  createSignedUrl(
    resourceId:"{resourceId}"
    objectName:"ortho-cog.tif"
  ) {
   signedUrl
  }
}
```

curl
```
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation{createSignedUrl(resourceId:\"{resourceId}\" objectName:\"ortho-cog.tif\"){signedUrl}}"}' \
https://api.pointscene.com/graphql
```