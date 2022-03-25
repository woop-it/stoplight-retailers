---
tags: ['Bases']
---

# Authentication

A token is required to interact with our APIs. Once retrieved, it is valid for 24 hours and must be provided in an HTTP header for each call: `Authorisation: Bearer {token}`

### URLs

| Environment |                             URL                            |
| ------------- | :--------------------------------------------------------: |
| Production    |          <https://token.last-mile.fr/oauth/token>          |
| Preproduction | <https://connect.preprod.gcp.last-mile.fr/api/oauth/token> |
| Receipt       | <https://connect.recette.gcp.last-mile.fr/api/oauth/token> |

### Retrieving a token

<!-- theme: info -->

> 💡     The client_id and client_secret parameters will be provided later. 

<!-- theme: danger -->

>   For this call only, the Content-Type specified in the header must be **application/x-www-form-urlencoded**.


```json http
{
  "method": "post",
  "url": "https://token.last-mile.fr/oauth/token",
  "headers": {
    "Content-Type": "application/x-www-form-urlencoded"
  },
  "body": {
    "client_id": "XXXXXXXXXXXXXXX",
    "client_secret": "XXXXXXXXXXXXXXXX",
    "audience": "https://retailer.last-mile.fr/",
    "grant_type": "client_credentials"
  }
}
```
#### Response
```json json_schema
{
  "type": "object",
  "description": "Token",
  "properties": {
    "access_token": {
      "type": "string",
      "description": "Token to be retrieved and provided in the Header Authorisation"
    },
    "token_type": {
      "type": "string",
      "enum": [
        "bearer"
      ]
    },
    "expires_in": {
      "type": "number",
      "description": "Token expiration in ms"
    },
    "audience": {
      "type": "string"
    }
  },
  "required": [
    "access_token",
    "token_type",
    "expires_in"
  ]
}
```
