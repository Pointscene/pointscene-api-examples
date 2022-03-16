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
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2NDc0NDMyODYsImV4cCI6MTY0NzQ1NzY4Niwic3ViIjoidXNlci92cVNsIiwianRpIjoiZjQwZDkyZmMtMzc5MC00OTA5LWExZmQtMTlkODI2OTY3ODIxIn0.-Fg30iv3E0GXljZOHyvG7aClCdSxkzMrKtIm8OMgYkY" \
-d '{"query": "mutation{createSignedUrl(resourceId:\"{resourceId}\" objectName:\"ortho-cog.tif\"){signedUrl}}"}' \
https://api.pointscene.com/graphql
```