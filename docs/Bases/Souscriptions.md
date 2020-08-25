# Souscriptions


Le système de souscriptions permet de **s'abonner à des événements** liés à vos commandes qui se passe sur la plateforme Woop.

Par exemple : Mis à jour du statut ou choix du transporteur de votre commande.


Ces évènements sont décrits dans la partie **Woop vers Enseigne** de notre documentation.

## Initialisation des échanges


Pour vous abonner aux divers événements un premier appel à **l'API [/souscriptions](https://woop.stoplight.io/docs/retailer/retailer_to_woop.v1.4.0.json/paths/~1subscriptions/post)** est nécessaire.

Les données à envoyées sont :

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
          "description": "Callback permettant de recevoir le choix du transporteur."
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
          "description": "Callback permettant de recevoir les notes client"
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
          "description": "Callback permettant de recevoir les informations de facturation"
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
          "description": "Callback permettant de recevoir les notifications envoyées au client"
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

Les `callbacks` ou autrement dit `webhooks` permettent de définir l'URL appelée lors des divers événements, différents callbacks sont possible sur notre plateforme :


Callback  | Description | Endpoint | Requis
---------|----------|---------
carrier | Callback permettant de recevoir le choix du transporteur | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put) | **OUI**
status | Callback permettant de recevoir les changements de statut | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put) | **OUI**
score | Callback permettant de recevoir les notes client | [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put) | **OUI**
deliveryClosure | Callback permettant de recevoir les informations de facturation | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NON
event | Callback permettant de recevoir les notifications envoyées au client | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post) | NON

### Composition d'un callback

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
> Pour récupérer l'orderId dans vos APIs, il est fortement conseillé d’incorporer la variable `{orderId}` dans vos urls > de callbacks.
> Cette variable sera remplacé par la valeur de l'orderId lors des appels.
>
> Exemple: **https://my_url/orders/{orderId}/status** 

**Version**

Version d'API ciblé du callback.

Comme toutes nos APIs, les callbacks sont versionnés, **lorsque vous souscrivez à un callback il faut préciser à quelle version**.

La version est disponible dans la documentation [Woop vers Enseigne](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json).

