# Authentication
## Create access token for Client
```
POST /oauth2/token HTTP/1.1
Host: https://api.pointscene.com
 
grant_type=client_credentials
&client_id={client_id}
&client_secret={secret}
&scope={scope}
```

Curl example command:
```
$ curl \
-X POST \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "grant_type=client_credentials&client_id={client_id}&client_secret={secret}&scope=instance-write-{instance_id}" \
https://api.pointscene.com/oauth2/token
```

Clients require scope and available scopes are:
```
instance-* - Write access to all linked instances. Wildcard scope does not expire
instance-write-{instance_id} - Write access to an instance and its entities
instance-read-{instance_id} - Read access to an instance and its entities
instance-create - Can create a new instance
resource-write-{resource_id} - Write access to a resource
resource-read-{resource_id} - Read access to a resource
```

## Response for Client token

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
 
{
 "access_token":"eyJhbGc...",
 "expires_in":14399,
 "token_type":"Bearer",
}
```

## Crete access token for User
```
POST /oauth2/token HTTP/1.1
Host: https://api.pointscene.com
 
grant_type=password
&username={user}
&password={pwd}
&client_id={client_id}
```

Curl example command:

``` 
$ curl \
-X POST \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "grant_type=password&username={user}&password={pwd}&client_id={client_id}" \
https://api.pointscene.com/oauth2/token
```

## Refresh token
```
POST /oauth2/token HTTP/1.1
Host: https://api.pointscene.com
 
grant_type=refresh_token
&client_id={client_id}
&refresh_token={token}
```

Curl example command:
```
$ curl \
-X POST \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "grant_type=refresh_token&client_id={client_id}&refresh_token={token}" \
https://api.pointscene.com/oauth2/token
```

## Response for User token

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
 
{
 "access_token":"eyJhbGc...",
 "refresh_token":"r6pIf...",
 "expires_in":14399,
 "token_type":"Bearer",
}
```