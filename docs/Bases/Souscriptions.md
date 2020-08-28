---
tags: ['Bases']
---

# Souscriptions


Le système de souscriptions permet de **s'abonner à des événements** liés à vos commandes qui se passent sur la plateforme Woop.

Par exemple : Mise à jour du statut ou choix du transporteur de votre commande.


Ces évènements sont décrits dans la partie **Woop vers Enseigne** de notre documentation.

## Initialisation des souscriptions


Pour vous abonner aux évènements un premier appel à **l'API [/souscriptions](https://woop.stoplight.io/docs/retailer/retailer_to_woop.v1.4.0.json/paths/~1subscriptions/post)** est nécessaire.

Les données à envoyer sont :

```json json_schema
{
  "type": "object",
  "description": "Informations de souscriptions",
  "required": [
    "callbacks"
  ],
  "properties": {
    "callbacks": {
      "type": "object",
      "description" : "Callbacks des événements",
      "required": [
        "carrier",
        "status",
        "score"
      ],
      "properties": {
        "carrier": {
          "type": "object",
          "description": "Callback permettant de recevoir le choix du transporteur.",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "Url de la route d'API"
            },
            "version": {
              "type": "string",
              "description": "Version d'API pour ce callback",
              "example": "1.1.0"
            }
          }
        },
        "status": {
          "type": "object",
          "required": [
            "url"
          ],
          "description": "Callback permettant de recevoir les changements de statut",
          "properties": {
            "url": {
                "type": "string",
                "description": "Url de la route d'API"
            },
            "version": {
              "type": "string",
              "description": "Version d'API pour ce callback",
              "example": "1.1.0"
            }
          }
        },
        "score": {
          "type": "object",
          "description": "Callback permettant de recevoir les notes client",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "Url de la route d'API."
            },
            "version": {
              "type": "string",
              "description": "Version d'API pour ce callback.",
              "example": "1.1.0"
            }
          }
        },
        "deliveryClosure": {
          "type": "object",
          "description": "Callback permettant de recevoir les informations de facturation",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "Url de la route d'API."
            },
            "version": {
              "type": "string",
              "description": "Version d'API pour ce callback",
              "example": "1.1.0"
            }
          }
        },
        "event": {
          "type": "object",
          "description": "Callback permettant de recevoir les notifications envoyées au client",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "Url de la route d'API"
            },
            "version": {
              "type": "string",
              "description": "Version d'API pour ce callback",
              "example": "1.1.0"
            }
          }
        }
      }
    },
    "headers": {
      "type": "array",
      "description": "Headers HTTP supplémentaires à envoyer lors des callbacks",
      "items": {
        "type": "object",
        "required": [
          "key",
          "value"
        ],
        "properties": {
          "key": {
            "type": "string",
            "description": "Clé/nom du header"
          },
          "value": {
            "type": "string",
            "description": "Valeur du header"
          }
        }
      }
    },
    "auth": {
      "type": "object",
      "description": "Configuration de l'authentification à votre API",
      "properties": {
        "basic": {
          "type": "object",
          "description": "A definir si la méthode d'authentification à l'API voulue est basic",
          "required": [
            "username",
            "password"
          ],
          "properties": {
            "username": {
              "type": "string"
            },
            "password": {
              "type": "string"
            }
          }
        },
        "oauth2": {
          "type": "object",
          "description": "A definir si la méthode d'authentification à l'API voulue est oauth2",
          "required": [
            "client_id",
            "client_secret",
            "tokenEndPoint"
          ],
          "properties": {
            "client_id": {
              "type": "string"
            },
            "client_secret": {
              "type": "string"
            },
            "audience": {
              "type": "string"
            },
            "grant_type": {
              "type": "string"
            },
            "tokenEndPoint": {
              "type": "string",
              "description": "Url permettant de recupérer le token d'accès en fonction du clientId et du clientSecret"
            }
          }
        },
        "token": {
          "type": "object",
          "description": "A définir si la méthode d'authentification donne un bearer token à partir d'un username/password",
          "required": [
            "username",
            "password",
            "endpoint"
          ],
          "properties": {
            "username": {
              "type": "string"
            },
            "password": {
              "type": "string"
            },
            "endpoint": {
              "type": "string",
              "description": "Url permettant de recupérer le token d'accès"
            }
          }
        }
      }
    }
  }
}
```

### Callbacks

Les `callbacks` ou autrement dit `webhooks` permettent de définir l'URL appelée pour chaque événement, différents callbacks sont disponibles **dont certains sont obligatoires** :


Callback  | Description | Contrat d'interface | Requis
---------|----------|---------
carrier | Callback permettant de recevoir le choix du transporteur | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put) | **OUI**
status | Callback permettant de recevoir les changements de statut | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put) | **OUI**
score | Callback permettant de recevoir les notes client | [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put) | **OUI**
deliveryClosure | Callback permettant de recevoir les informations de facturation | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NON
event | Callback permettant de recevoir les notifications envoyées au client | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post) | NON

**Description d'un callback**

```json json_schema
{
  "type": "object",
  "description": "Callback"
  "required": [
    "url"
  ],
  "properties": {
    "url": {
      "type": "string",
      "description": "Url de la route d'API"
    }, 
    "version": {
      "type": "string",
      "description": "Version d'API pour ce callback",
      "example": "1.1.0"
    }
  }
}
```

**Url**

Url de la route d'API vers laquelle la plateforme Woop enverra l’événement lié au callback.

<!-- theme: info -->

> **Variable d'url**
>
> Pour récupérer l'orderId dans vos APIs, il est fortement conseillé d’incorporer la variable `{orderId}` dans vos urls de callbacks.
> Cette variable sera remplacée par la valeur de l'orderId lors des appels.
>
> Exemple: **https://my_url/orders/{orderId}/status** 

**Version**

Version d'API ciblée du callback.

Comme toutes nos APIs, les callbacks sont versionnées, **lorsque vous souscrivez à un callback il faut préciser à quelle version**.

La version est disponible dans la documentation [Woop vers Enseigne](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json).

Exemple :
```json
{
  "callbacks": {
    "status" : {
      "url": "https://my_url/orders/{orderId}/status",
      "version": "1.1.0"
    }
  }
}
```


### Headers

Si votre API a besoin de headers HTTP supplémentaires, il est possible de configurer plusieurs couples de clé-valeur qui seront envoyés à chaque appel.

Exemple :
```json
{
  "headers" : [
    {
      "x-api-key": "78YJHBG738knkh3"
    }
  ]
}
```

### Auth

Si votre API nécessite une authentification, il est possible de la configurer.

Trois méthodes d’authentification sont disponibles :


<!--
type: tab
title: Méthode Basic
-->
Configuration:
```json
{
  "auth": {
    "basic": {
      "username": "admin",
      "password": "1234"
    }
  }
}
```
Un header HTTP `Authorization : Basic YWRtaW46MTIzNA==` sera envoyé à votre API.

`YWRtaW46MTIzNA==` étant la représentation en Base64 du texte admin:1234
<!--
type: tab
title: Méthode OAuth2
-->
Configuration:
```json
{
  "auth": {
    "oauth2": {
      "client_id": "XXXXXXXXXXX",
      "client_secret": "xxxxxxXXXXXXx",
      "audience": "my-audience.fr",
      "grant_type": "client_credentials",
      "tokenEndPoint": "https://my-token-url.fr"
    }
  }
}
```
Un échange de token respectant la spécification [OAuth2 client_credentials](https://tools.ietf.org/html/rfc6749#section-4.4) sera effectué à chaque appel.

<!--
type: tab
title: Méthode Token
-->
Configuration:
```json
{
  "auth": {
    "token": {
      "token": {
      "username": "admin",
      "password": "1234",
      "endpoint": "https://my-token-url.fr"
    }
  }
}
```
Cette méthode effectuera un appel **HTTP POST** vers l'endpoint configuré avec les paramètres suivants :
```json
{
  "username": "{username}",
  "password": "{password}"
}
```
Le endpoint appelé devra retourner un token : 
```json
{
  "token": "87YB1K2B312K3",
}
```
Ce token sera envoyé dans le header HTTP `Authorization: Bearer {token}`
<!-- type: tab-end -->


### Exemples de souscriptions

<!--
type: tab
title: Exemple 1
-->
Je m'abonne aux souscriptions obligatoires, mon API est protégée par une simple API Key.
```json
{
  "callbacks": {
    "carrier": {
      "url": "https://my_url/orders/{orderId}/carrier",
      "version": "1.1.0"
    },
    "status": {
      "url": "https://my_url/orders/{orderId}/status",
      "version": "1.1.0"
    },
    "score": {
      "url": "https://my_url/orders/{orderId}/score",
      "version": "1.1.0"
    }
  },
  "headers": [
    {
      "x-api-key": "514541VVNB"
    }
  ]
}
```

<!--
type: tab
title: Exemple 2
-->
Je m'abonne à toutes les souscriptions, mon API est protégée par une authentification OAuth2.
```json
{
  "callbacks": {
    "carrier": {
      "url": "https://my_url/orders/{orderId}/carrier",
      "version": "1.1.0"
    },
    "status": {
      "url": "https://my_url/orders/{orderId}/status",
      "version": "1.1.0"
    },
    "score": {
      "url": "https://my_url/orders/{orderId}/score",
      "version": "1.1.0"
    },
    "deliveryClosure": {
      "url": "https://my_url/orders/{orderId}/deliveryClosure",
      "version": "1.1.0"
    },
    "event": {
      "url": "https://my_url/orders/{orderId}/events",
      "version": "1.1.0"
    },
  },
  "auth": {
    "oauth2": {
      "client_id": "XXXXXXXXXXX",
      "client_secret": "xxxxxxXXXXXXx",
      "audience": "my-audience.fr",
      "grant_type": "client_credentials",
      "tokenEndPoint": "https://my-token-url.fr"
    }
  }
}
```

<!-- type: tab-end -->

## Implémentation des souscriptions

Pour chaque *callback* configuré il est nécessaire d'implémenter le contrat d'interface lié à celui-ci.

Pour rappel :

Callback  | Contrat d'interface | Requis
---------|----------|---------
carrier  | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put) | **OUI**
status | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put) | **OUI**
score |  [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put) | **OUI**
deliveryClosure | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NON
event | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post) | NON


<!-- theme: warning -->

> **Méthodes et codes HTTP**
>
> Lors de l'implémentation des contrats d'interfaces, il est **important** de bien respecter les **méthodes HTTP** (POST. PATCH etc...) ainsi que les **codes HTTP retours** (201, 400 etc..) spécifiés dans le contrat d'interface.