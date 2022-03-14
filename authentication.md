# Authentication
## Create access token for Client
```
POST oauth2/token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=client_credentials
&client_id={client_id}
&client_secret={secret}
&scope=instance-write-{instance_id}
```

Curl example command:
```
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&client_id={client_id}&client_secret={secret}&scope=instance-write-{instance_id}" https://api.pointscene.com/oauth2/token
```

Clients can be granted scoped access. Available scopes for client access are:
```
instance-read-{id} - Read access to an instance and its entities
instance-write-{id} - Write access to an instance and its entities
instance-create - Can create a new instance
```

## Crete access token for User
```
POST oauth2/token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=password
&username={user}
&password={pwd}
&client_id={client_id}
```

Curl example command:

``` 
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=password&username={user}&password={pwd}&client_id={client_id}" https://api.pointscene.com/oauth2/token
```

## Refresh token
```
POST oauth2/token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=refresh_token
&client_id={client_id}
&refresh_token={token}
```

Curl example command:
```
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=refresh_token&client_id={client_id}&refresh_token={token}" https://api.pointscene.com/oauth2/token
```

## Response

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
 
{
 "access_token":"eyJhbGc...",
 "refresh_token":"r6pIf...",
 "expires_in":14399,
 "token_type":"Bearer",
}
```