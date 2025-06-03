# Add configuration
### Set up the resource with the necessary authentication configuration
GraphQL
```
mutation{
  addJobConfig(
    resourceId:"{resourceId}"
    config: {
      drive:{
        type: "drive"
        client_id: "{CLIENT_ID}"
        client_secret: "{CLIENT_SECRET}"
        scope: "drive"
        token:"{\"access_token\":\"sl.BfH6SMA...\",\"token_type\":\"Bearer\",\"refresh_token\":\"sl.0gH3...\",\"expiry\":\"2025-05-20T14:45:00.123456789Z\"}"
      }
      dropbox:{
        type: "dropbox"
        app_key: "{APP_KEY}"
        app_secret: "{APP_SECRET}"
        token: "{\"access_token\":\"sl.BfH6SMA...\",\"token_type\":\"Bearer\",\"refresh_token\":\"sl.0gH3...\",\"expiry\":\"2025-05-20T14:45:00.123456789Z\"}"
      }
      aws_s3:{
        type: "s3"
        provider: "AWS"
        access_key_id: "{ACCESS_KEY}"
        secret_access_key: "{SECRET_KEY}"
        region: "{REGION}"
      }
      acc:{
        type: "acc"
        token:"{\"access_token\":\"eyJ...\",\"token_type\":\"Bearer\",\"refresh_token\":\"77Glm...\",\"expiry\":\"2025-06-01T14:46:35.791030264+02:00\",\"expires_in\":3779}"
        hub_id: "b.2b7f...\"
        project_id: "b.0b55...\"
      }
    }
  ) {
    success
  }
}
```
curl
```
curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {YOUR_AUTH_TOKEN}" \
  -d '{
    "query": "mutation { addJobConfig(resourceId: \"{resourceId}\", config: { drive: { type: \"drive\", client_id: \"{CLIENT_ID}\", client_secret: \"{CLIENT_SECRET}\", scope: \"drive\", token: \"{\\\"access_token\\\":\\\"sl.BfH6SMA...\\\",\\\"token_type\\\":\\\"Bearer\\\",\\\"refresh_token\\\":\\\"sl.0gH3...\\\",\\\"expiry\\\":\\\"2025-05-20T14:45:00.123456789Z\\\"}\" }, dropbox: { type: \"dropbox\", app_key: \"{APP_KEY}\", app_secret: \"{APP_SECRET}\", token: \"{\\\"access_token\\\":\\\"sl.BfH6SMA...\\\",\\\"token_type\\\":\\\"Bearer\\\",\\\"refresh_token\\\":\\\"sl.0gH3...\\\",\\\"expiry\\\":\\\"2025-05-20T14:45:00.123456789Z\\\"}\" }, aws_s3: { type: \"s3\", provider: \"AWS\", access_key_id: \"{ACCESS_KEY}\", secret_access_key: \"{SECRET_KEY}\", region: \"{REGION}\" }, acc: { type: \"acc\", token: \"{\\\"access_token\\\":\\\"eyJ...\\\",\\\"token_type\\\":\\\"Bearer\\\",\\\"refresh_token\\\":\\\"77Glm...\\\",\\\"expiry\\\":\\\"2025-06-01T14:46:35.791030264+02:00\\\",\\\"expires_in\\\":3779}\", hub_id: \"b.2b7f...\", project_id: \"b.0b55...\" } }) { success } }"
  }' \
  https://api.pointscene.com/graphql
```