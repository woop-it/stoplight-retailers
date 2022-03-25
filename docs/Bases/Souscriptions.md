---
tags: ['Bases']
---

# Subscriptions


The subscription system allows you to **subscribe to events** related to your orders on the Woop platform.

For example: Update the status or choose the carrier for your order.


These events are described in the section **Woop to Brand** in our documentation.

## Initiating subscriptions


To subscribe to events, a first call to **the API [/subscriptions](https://woop.stoplight.io/docs/retailer/retailer_to_woop.v1.4.0.json/paths/paths/~1subscriptions/post)** is required.

The data to be sent is:

```json json_schema
{
  "type": "object",
  "description": "Subscription information",
  "required": [
    "callbacks"
  ],
  "properties": {
    "callbacks": {
      "type": "object",
      "description" : "Event callbacks",
      "required": [
        "carrier",
        "status",
        "score"
      ],
      "properties": {
        "carrier": {
          "type": "object",
          "description": "Callback to receive the choice of carrier.",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route"
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
          "description": "Callback to receive status changes",
          "properties": {
            "url": {
                "type": "string",
                "description": "URL of the API route"
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
          "description": "Callback to receive customer ratings",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route."
            },
            "version": {
              "type": "string",
              "description": "API version for this callback.",
              "example": "1.1.0"
            }
          }
        },
        "deliveryClosure": {
          "type": "object",
          "description": "Callback to receive billing information",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route."
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
          "description": "Callback to receive notifications sent to the customer",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "deltaCosts": {
          "type": "object",
          "description": "Callback to receive deltaCost information on the order issued by the carrier.",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "quote": {
          "type": "object",
          "description": "Callback to receive quotes from carriers",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route"
            },
            "version": {
              "type": "string",
              "description": "API version for this callback",
              "example": "1.1.0"
            }
          }
        },
        "collectStatus": {
          "type": "object",
          "description": "Callback to receive changes in the status of a collection",
          "required": [
            "url"
          ],
          "properties": {
            "url": {
              "type": "string",
              "description": "URL of the API route"
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
      "description": "Additional HTTP headers to be sent in callbacks",
      "items": {
        "type": "object",
        "required": [
          "key",
          "value"
        ],
        "properties": {
          "key": {
            "type": "string",
            "description": "Key/name of the header"
          },
          "value": {
            "type": "string",
            "description": "Value of the header"
          }
        }
      }
    },
    "auth": {
      "type": "object",
      "description": "Configuring the authentication of your API",
      "properties": {
        "basic": {
          "type": "object",
          "description": "To be defined if the required API authentication method is basic",
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
          "description": "To be defined if the required API authentication method is oauth2",
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
              "description": "URL to retrieve the access token according to the clientId and the clientSecret"
            }
          }
        },
        "token": {
          "type": "object",
          "description": "To be defined if the authentication method gives a bearer token from a username/password",
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
              "description": "URL to retrieve the access token"
            }
          }
        }
      }
    }
  }
}
```

### Callbacks

`Callbacks` also known as `webhooks` allow you to define the URL called for each event, different callbacks are available **some of which are mandatory**:

Callback  | Interface contract | Required
---------|----------|---------
carrier  | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put) | NO
status | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put) | NO
score |  [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put) | NO
deliveryClosure | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NO
event | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post) | NO
deltaCost |  [/orders/{orderId}/deltaCost](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deltaCosts/post) | NO
quote | [/orders/{orderId}/quote](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1quotes/post) | NO
collectStatus | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1collects~1%7BcollectId%7D~1status/put) | NO


**Description of a callback**

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
      "description": "URL of the API route"
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

URL of the API route where the Woop platform sends the callback event.

<!-- theme: info -->

> **URL variable**
>
> To retrieve the orderId in your APIs, it is highly recommended to include the variable `{orderId}` in your callback URLs.
> This variable will be replaced by the value of the orderId in calls.
>
> Exemple: **https://my_url/orders/{orderId}/status** 

**Version**

Targeted API version of the callback.

Like all our APIs, callbacks are versioned, **when you subscribe to a callback you must specify which version**.

The version is found in the documentation [Woop to Brand](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json).

Example:
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

If your API needs additional HTTP headers, you can add multiple key-value pairs to be sent on each call.

Example:
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

Your API can be configured if it requires authentication.

Three authentication methods are available:


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
An HTTP header `Authorisation: Basic YWRtaW46MTIzNA==` will be sent to your API.

`YWRtaW46MTIzNA==` Which is the Base64 representation of the text admin:1234
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
A token exchange that complies with the [OAuth2 client_credentials](https://tools.ietf.org/html/rfc6749#section-4.4) will be made for each call.

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
This method will make a call **HTTP POST** to the endpoint configured with the following parameters:
```json
{
  "username": "{username}",
  "password": "{password}"
}
```
The called endpoint should return a token: 
```json
{
  "token": "87YB1K2B312K3",
}
```
This token will be sent in the HTTP header `Authorisation: Bearer {token}`
<!-- type: tab-end -->


### Example subscriptions

<!--
type: tab
title: Example 1
-->
I subscribe to the required subscriptions, my API is protected by a simple API Key.
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
I subscribe to the required subscriptions, my API is protected by authentication, it is possible to configure it OAuth2.
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

## Subscription implementation

For each *callback* configured you must implement the interface contract linked to it.

As a reminder:

Callback  | Interface contract | Required
---------|----------|---------
carrier  | [/orders/{orderId}/carrier](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1carrier/put) | NO
status | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1status/put) | NO
score |  [/orders/{orderId}/score](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1score/put) | NO
deliveryClosureosure | [/orders/{orderId}/deliveryClosure](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deliveryClosure/post) | NO
event | [/orders/{orderId}/events](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1events/post) | NO
deltaCost |  [/orders/{orderId}/deltaCost](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1deltaCosts/post) | NO
quote | [/orders/{orderId}/quote](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1orders~1%7BorderId%7D~1quotes/post) | NO
collectStatus | [/orders/{orderId}/status](https://woop.stoplight.io/docs/retailer/woop_to_retailer.v1.1.0.json/paths/~1collects~1%7BcollectId%7D~1status/put) | NO


<!-- theme: warning -->

> **HTTP methods and codes**
>
> When implementing interface contracts, it is **important** to use **HTTP methods** (POST. PATCH etc.) and the **HTTP return codes** (201, 400 etc.) specified in the interface contract.