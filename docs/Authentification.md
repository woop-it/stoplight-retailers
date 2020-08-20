# Authentification

Un token est nécessaire pour échange avec nos APIs, une fois récupéré il est valide pendant 24h et doit être fourni à chaque appel dans un header HTTP : ``` Authorization: Bearer {token} ```


### Urls

| Environnement |      Url     |
| ------------- | :-----------: |
| Production    | <https://token.last-mile.fr/oauth/token> |
| Preproduction | <https://connect.preprod.gcp.last-mile.fr/api/oauth/token> |
| Recette       | <https://connect.recette.gcp.last-mile.fr/api/oauth/token> |

### Récupérer un token
<!-- theme: info -->

> 💡   &nbsp; Les paramètres client_id et client_secret vous seront communiqués ultérieurement.

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