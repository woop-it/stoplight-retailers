---
tags: ["Basics"]
---

# Subscriptions

Subscription system allows you to **subscribe to requests and events** related to order transitions on Woop platform.

For example : Status update or carrier choice for your order.

Those requests and events are described in **Woop to Retailer** section of our documentation.

## Subscription initialization

To subscribe to requests and events, you will need to make a first call to **API [/subscriptions](https://woop.stoplight.io/docs/retailer/branches/english/retailer_to_woop.v1.4.0.json/paths/~1subscriptions/post)**.


```json json_schema
{
  "type": "object",
  "description": "Subscription informations",
  "required": [
    "callbacks"
  ],
  "properties": {
    "callbacks": {
      "type": "object",
      "description" : "Events callbacks",
      "required": [
        "carrier",
        "status",
        "score"
      ],
      "properties": {
        "carrier": {
          "type": "object",
          "description": "Callback allowing to receive carrier choice.",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "API route URL"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "status": {
          "type": "object",
          "required": [
            "url"
          ],
          "description": "Callback allowing to receive order status changes.",
          "properties": {
            "url": {
                "type": "string",
                "description": "API route URL"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "score": {
          "type": "object",
          "description": "Callback allowing to receive the customer notation",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "API route URL"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "deliveryClosure": {
          "type": "object",
          "description": "Callback allowing to receive the billing informations",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "API route URL"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "event": {
          "type": "object",
          "description": "Callback allowing to receive the notifications send to customer",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "API route URL"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        }
      }
    },
    "headers": {
      "type": "array",
      "description": "Additional HTTP Headers to send during callbacks",
      "items": {
        "type": "object",
        "required": [
          "key",
          "value"
        ],
        "properties": {
          "key": {
            "type": "string",
            "description": "Header key/name"
          },
          "value": {
            "type": "string",
            "description": "Header value"
          }
        }
      }
    },
    "auth": {
      "type": "object",
      "description": "Configuration of your API authentication",
      "properties": {
        "basic": {
          "type": "object",
          "description": "To be defined if you choose basic API authentication method",
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
          "description": "To be defined if you choose oauth2 API authentication method",
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
              "description": "Url used to retrieve the access token according to clientId and clientSecret"
            }
          }
        },
        "token": {
          "type": "object",
          "description": "To be defined if the authentication method gives a bearer token from a username/password combination",
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
              "description": "Url used to retrieve the access token"
            }
          }
        }
      }
    }
  }
}
```

### Callbacks

`Callbacks` or in other words `webhooks` allow to define the called URL for each request or event. Different callbacks are available, **some of which are mandatory** :

Callback | Description | Interface contract | Required
---------|-------------|--------------------|---------
carrier         | Callback allowing receiving carrier choice               | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put)                  | **YES**
status          | Callback allowing receiving status updates               | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put)                    | **YES**
score           | Callback allowing receiving client rating                | [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put)                      | **YES**
deliveryClosure | Callback allowing receiving billing informations         | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NO
event           | Callback allowing receiving notifications sent to client | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post)                   | NO

**Callback description**

```json json_schema
{
  "type": "object",
  "description": "Callback",
  "required": ["url"],
  "properties": {
    "url": {
      "type": "string",
      "description": "API route URL"
    },
    "version": {
      "type": "string",
      "description": "API version for this callback",
      "example": "1.1.0"
    }
  }
}
```

**URL**

API route URL to which Woop will send the event linked to the callback.

<!-- theme: info -->

> **URL variable**
>
> To retrieve orderId in your APIs, it is strongly suggested to integrate variable `{orderId}` in your callbacks URLs.
> This variable will be replaced by its real value during calls.
>
> Example: **https://my_url/orders/{orderId}/status**

**Version**

The version of the targeted API callback.

Like all our APIs, callbacks are versioned, **when you subsribe to a callback, you must specify a version**.

The version is available in the documentation [Woop to Retailer](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json).

Example :

```json
{
  "callbacks": {
    "status": {
      "url": "https://my_url/orders/{orderId}/status",
      "version": "1.1.0"
    }
  }
}
```

### Headers

If your API needs additional HTTP Headers, it is possible to configure key/value couples that will be sent at each call.

Example :

```json
{
  "headers": [
    {
      "x-api-key": "78YJHBG738knkh3"
    }
  ]
}
```

### Auth

If your API needs an authentication, it is possible to configure it.

3 authentication methods are available :

<!--
type: tab
title: Basic method
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

An HTTP Header `Authorization : Basic YWRtaW46MTIzNA==` will be sent to your API.

`YWRtaW46MTIzNA==` being the Base64 representation of text admin:1234

<!--
type: tab
title: OAuth2 method
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

A token exchange according to specification [OAuth2 client_credentials](https://tools.ietf.org/html/rfc6749#section-4.4) will be made at each call.

<!--
type: tab
title: Token method
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

This method will make an **HTTP POST** to configured endpoint with following parameters :

```json
{
  "username": "{username}",
  "password": "{password}"
}
```

Called endpoint must answer a token :

```json
{
  "token": "87YB1K2B312K3"
}
```

This token will be sent in HTTP Header `Authorization: Bearer {token}`

<!-- type: tab-end -->

### Subscription examples

<!--
type: tab
title: Example 1
-->

I subscribe to mandatory callbacks, my API is protected by a simple API key.

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
title: Example 2
-->

I subscribe to all callbacks, my API is protected by an OAuth2 authentication.

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
    }
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

## Subscriptions implementation

For each configured _callback_, it is necessary to implement the interface contract related to it.

Reminder :

Callback | Interface contract | Required
---------|--------------------|---------
carrier   | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put)                  | **YES**
status    | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put)                    | **YES**
score     | [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put)                      | **YES**
deliveryClosure | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NO
event     | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post)                   | NO

<!-- theme: warning -->

> **Methods and HTTP codes**
>
> During the implementation of interface contracts, it is **important** to respect **HTTP methods** (POST, PATCH , etc.) and **HTTP response codes** (201, 400, etc.) specified in interface contract.
