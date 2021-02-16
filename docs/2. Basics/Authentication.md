---
tags: ["Basics"]
---

# Authentication

A token is needed to communicate with our APIs, once taken its valid during 24H et must be provided in each call in a HTTP Header: `Authorization: Bearer {token}`

### URLs

| Environment    |                            URL                             |
| -------------- | :--------------------------------------------------------: |
| Production     |          <https://token.last-mile.fr/oauth/token>          |
| Pre-production | <https://connect.preprod.gcp.last-mile.fr/api/oauth/token> |
| Staging        | <https://connect.recette.gcp.last-mile.fr/api/oauth/token> |

### Retrieve a token

<!-- theme: info -->

> 💡 &nbsp; Parameters `client_id` and `client_secret` will be communicated later to you by Woop IT team.

<!-- theme: danger -->

> Only for this call, defined Content-Type in header must be **application/x-www-form-urlencoded**.

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
      "description": "Token to provide in Authorization Header"
    },
    "token_type": {
      "type": "string",
      "enum": ["bearer"]
    },
    "expires_in": {
      "type": "number",
      "description": "Token expiration in ms"
    },
    "audience": {
      "type": "string"
    }
  },
  "required": ["access_token", "token_type", "expires_in"]
}
```
