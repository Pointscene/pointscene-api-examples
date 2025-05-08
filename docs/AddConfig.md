# Add configuration
### Configure the resource with authentication credentials
GraphQL
```
mutation{
  addSyncConfig(
    resourceId:"{resourceId}"
	config:"-----BEGIN PGP MESSAGE-----\n\nhQGMA2HEb2Bk13er..."
  ) {
    success
  }
}
```
curl
```
$ curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {TOKEN}" \
-d '{"query": "mutation { addSyncConfig(resourceId: \"{resourceId}\", config: \"-----BEGIN PGP MESSAGE-----\\n\\nhQGMA2HEb2Bk13er...\") { success } }"}' \
https://api.pointscene.com/graphql
```