---
tags: ['Bases']
---

# Authentification

Un token est nécessaire pour échanger avec nos APIs, une fois récupéré il est valide pendant 24h.

## Récupérer un token

### Urls

| Environnement |                             Url                            |
| ------------- | :--------------------------------------------------------: |
| Production    |          <https://token.last-mile.fr/oauth/token>          |
| Preproduction | <https://connect.preprod.gcp.last-mile.fr/api/oauth/token> |
| Recette       | <https://connect.recette.gcp.last-mile.fr/api/oauth/token> |


<!-- theme: info -->

> 💡     Les paramètres client_id et client_secret vous seront communiqués ultérieurement. 

<!-- theme: danger -->

>   Pour cet appel uniquement le Content-Type précisé dans le header doit être **application/x-www-form-urlencoded**.


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
### Réponse
```json json_schema
{
  "type": "object",
  "description": "Token",
  "properties": {
    "access_token": {
      "type": "string",
      "description": "Token à récuperer et à fournir dans le Header Authorization"
    },
    "token_type": {
      "type": "string",
      "enum": [
        "bearer"
      ]
    },
    "expires_in": {
      "type": "number",
      "description": "Expiration du token en ms"
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

## Utiliser du token

L'`acces_token` obtenu doit être fourni à chaque appel dans un header HTTP : `Authorization: Bearer {token}`

### Urls de nos API

| Environnement |                             Url                            |
| ------------- | :--------------------------------------------------------: |
| Production    | <https://retailer.last-mile.fr>          |
| Preproduction | <https://ret-api.preprod.gcp.last-mile.fr> |
| Recette       | <https://ret-api.recette.gcp.last-mile.fr> |


