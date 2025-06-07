## User API

## Regster User

Endpoint : POST /api/users

Request Body :

```json
{
  "username" : "daffa",
  "pssword" : "secret",
  "name" : "Daffa Saputra"
}
```

Response Body (Success) :

```json
{
  "data" : "OK"
}
```

Response Body (Failed) :

```json
{
  "errors" : "Username must not blank !!!"
}
```


## Login User

Endpoint : POST /api/auth/login

Request Body :

```json
{
  "username" : "daffa",
  "pssword" : "secret"
}
```

Response Body (Success) :

```json
{
  "data" : {
    "token" : "TOKEN",
    "expiresAt" : 234234234234 
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "username or password wrong"
}
```
## Get User
Endpoint : GET /api/users/current

Request Header:

- X-API-TOKEN : Token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "username" : "daffa",
    "nama" : "Daffa Saputra"
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Unauthorized"
}
```

## Update User
Endpoint : PATHC /api/users/current

Request Header:

- X-API-TOKEN : Token (Mandatory)

Request Body :

```json
{
  "name" : "Daffa Saputra",
  "password" : "new password"
}

```
Response Body (Success) :

```json
{
  "data" : {
    "username" : "daffa",
    "nama" : "Daffa Saputra"
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Unauthorized"
}
```


## Logout User

Endpoint : DELETE /api/auth/logout

Request Header:

- X-API-TOKEN : Token (Mandatory)

Response Body (Success) :

```json
{
  "data" : "Ok"
}
```