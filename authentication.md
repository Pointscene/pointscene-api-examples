# Authentication
## Create access token for Client
```
POST /token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=client_credentials
&client_id=xxxxxxxxxx
&client_secret=xxxxxxxxxx
&scope=instance-write-xxxx
```

Curl example command:
```
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&client_id=xxxxxxxxxx&client_secret=xxxxxxxxxx&scope=instance-write-xxxxx" https://api.pointscene.com/oauth2/token
```

Clients can be granted scoped access. Available scopes for client access are:
```
instance-read-{id} - Read access to an instance and its entities
instance-write-{id} - Write access to an instance and its entities
instance-create - Can create a new instance
```

## Crete access token for User
```
POST /token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=password
&username=xxxxxxxxxx
&password=xxxxxxxxxx
&client_id=xxxxxxxxxx
```

Curl example command:

``` 
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=password&username=xxxxxxxxxx&password=xxxxxxxxxx&client_id=xxxxxxxxxx" https://api.pointscene.com/oauth2/token
```

## Refresh token
```
POST /token HTTP/1.1
Host: https://api.pointscene.com/oauth2/token
 
grant_type=refresh_token
&client_id=xxxxxxxxxx
&refresh_token=xxxxxxxxxx
```

Curl example command:
```
$ curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=refresh_token&client_id=xxxxxxxxxx&refresh_token=xxxxxxxxxx" https://api.pointscene.com/oauth2/token
```

Response

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
 
{
 "access_token":"xxxxxxxxxx",
 "refresh_token":"xxxxxxxxxx",
 "expires_in":3600,
 "token_type":"bearer",
}

```