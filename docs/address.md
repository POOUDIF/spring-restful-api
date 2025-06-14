# Address API Spec

## Create Address

Endpoint : POST /api/contacts/{idContact}/addresses

Request Header :

- X-API-TOKEN : Token (Mandatory)

Request Body :

```json
{
  "street": "Jalan",
  "city": "Kota",
  "province": "Provinsi",
  "country": "Negara",
  "postalCode": "12345"
}
```

Response Body (Success) :

```json
{
  "data": {
    "id": "random-string",
    "street": "Jalan",
    "city": "Kota",
    "province": "Provinsi",
    "country": "Negara",
    "postalCode": "12345"
  }
}
```

Response Body (Failed) :

```json
{
  "errors": "Address is not found"
}
```

## Update Address

Endpoint : PUT /api/contacts/{idContact}/addresses/{idAddress}

Request Header :

- X-API-TOKEN : Token (Mandatory)

Request Body :

```json
{
  "street": "Jalan apa",
  "city": "Kota",
  "province": "Provinsi",
  "country": "Negara",
  "postalCode": "12345"
}
```

Response Body (Success) :

```json
{
  "data": {
    "id": "random-string",
    "street": "Jalan apa",
    "city": "Kota",
    "province": "Provinsi",
    "country": "Negara",
    "postalCode": "12345"
  }
}
```

Response Body (Failed) :

```json
{
  "errors": "Address is not found"
}
```

## Get Address

Endpoint : GET /api/contacts/{idContact}/addresses/{idAddress}

Request Header :

- X-API-TOKEN : Token (Mandatory)

Response Body (Success) :

```json
{
  "data": {
    "id": "random-string",
    "street": "Jalan apa",
    "city": "Kota",
    "province": "Provinsi",
    "country": "Negara",
    "postalCode": "12345"
  }
}
```

Response Body (Failed) :

```json
{
  "errors": "Addresses is not found"
}
```

## Remove Address

Endpoint : DELETE /api/contacts/{idContact}/addresses/{idAddress}

Request Header :

- X-API-TOKEN : Token (Mandatory)

Response Body (Success) :

```json
{
  "data": "Ok"
}
```

Response Body (Failed) :

```json
{
  "errors": "Address is not found"
}
```

## List Address

Endpoint : GET /api/contacts/{idContact}/addresses

Request Header :

- X-API-TOKEN : Token (Mandatory)

Response Body (Success) :

```json
{
  "data": {
    "id": "random-string",
    "street": "Jalan apa",
    "city": "Kota",
    "province": "Provinsi",
    "country": "Negara",
    "postalCode": "12345"
  }
}
```

Response Body (Failed) :

```json
{
  "errors": "Addresses is not found"
}
```
