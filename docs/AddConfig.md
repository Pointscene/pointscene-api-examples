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
          app_key: "{YOUR_APP_KEY}"
          app_secret: "{YOUR_APP_SECRET}"
          token: "{\"access_token\":\"sl.BfH6SMA...\",\"token_type\":\"Bearer\",\"refresh_token\":\"sl.0gH3...\",\"expiry\":\"2025-05-20T14:45:00.123456789Z\"}"
        }
        aws_s3:{
          type: "s3"
          provider: "AWS"
          access_key_id: "{YOUR_ACCESS_KEY}"
          secret_access_key: "{YOUR_SECRET_KEY}"
          region: "{REGION}"
        }
        acc:{
          type: "acc"
          access_token:"eyJhb..." 
          token_type: "Bearer"
          expiry: "2025-05-09T13:38:17Z"
          refresh_token: "6On..."
          client_id: "{CLIENT_ID}"
          client_secret: "{CLIENT_SECRET}"
          hub_id: "b.2b7..."
          project_id: "b.0b5..."
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
    "query": "mutation { addJobConfig(resourceId: \"{resourceId}\", config: { drive: { type: \"drive\", client_id: \"{CLIENT_ID}\", client_secret: \"{CLIENT_SECRET}\", scope: \"drive\", token: \"{\\\"access_token\\\":\\\"sl.BfH6SMA...\\\",\\\"token_type\\\":\\\"Bearer\\\",\\\"refresh_token\\\":\\\"sl.0gH3...\\\",\\\"expiry\\\":\\\"2025-05-20T14:45:00.123456789Z\\\"}\" }, dropbox: { type: \"dropbox\", app_key: \"{YOUR_APP_KEY}\", app_secret: \"{YOUR_APP_SECRET}\", token: \"{\\\"access_token\\\":\\\"sl.BfH6SMA...\\\",\\\"token_type\\\":\\\"Bearer\\\",\\\"refresh_token\\\":\\\"sl.0gH3...\\\",\\\"expiry\\\":\\\"2025-05-20T14:45:00.123456789Z\\\"}\" }, aws_s3: { type: \"s3\", provider: \"AWS\", access_key_id: \"{YOUR_ACCESS_KEY}\", secret_access_key: \"{YOUR_SECRET_KEY}\", region: \"{REGION}\" }, acc: { type: \"acc\", access_token: \"eyJhb...\", token_type: \"Bearer\", expiry: \"2025-05-09T13:38:17Z\", refresh_token: \"6On...\", client_id: \"{CLIENT_ID}\", client_secret: \"{CLIENT_SECRET}\", hub_id: \"b.2b7...\", project_id: \"b.0b5...\" } }) { success } }"
  }' \
  https://api.pointscene.com/graphql
```