# Changelog


Toutes les modifications notables apportées aux apis seront documentées ici.

## Général

### 1.5 -> 1.6

#### Workflow statut de livraison
<!--
type: tab
title: 1.5
-->
![Workflow_status_livraison_1.5.png](https://stoplight.io/api/v1/projects/cHJqOjkyOTQ/images/S9Jyxo1wPbQ)


<!--
type: tab
title: 1.6
-->
![Workflow_status_livraison.png](https://stoplight.io/api/v1/projects/cHJqOjkyOTQ/images/uvZojBVFgns)
<!-- type: tab-end -->

## Enseigne vers Woop

### 1.5 -> 1.6

#### GET /orders 
[Lien vers la documentation](https://api.woopit.fr/docs/retailer/b3A6Njg0NzIwOA-recuperer-des-commandes)

- **Majeur**: Suppression des informations `packages` et `price`. Ces informations ne sont retournés que dans le détail d'une commande (get /orders/{id}). **/!\ Pas de rétro-compatibilité, suppression de ces informations sur toutes les versions !**


- **Majeur**: Remplacement du champs `currentStatus` par deux champs `status` et `subStatus` dans `delivery`: [Explication des nouveaux status de livraisons](https://api.woopit.fr/docs/retailer/ZG9jOjEwMDkzODc-statuts-de-livraison)

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      ...,
      "delivery": {
        "currentStatus": "DELIVERY_FAILED_WITH_RETURN"
      }
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "orders": [
    {
      ...,
      "delivery": {
        "status": "DELIVERY_KO",
        "subStatus": "FAILED_WITH_RETURN"
      }
    }
  ]
}
```
<!-- type: tab-end -->


- **Majeur**: Remplacement du champs `currentStatus` par un champs `status` dans `order`:

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      ...,
      "order": {
        "currentStatus": "ORDER_DELIVERED"
      }
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "orders": [
    {
      ...,
      "order": {
        "status": "ORDER_DELIVERED"
      }
    }
  ]
}
```
<!-- type: tab-end -->


#### GET /orders/{id}
[Lien vers la documentation](https://api.woopit.fr/docs/retailer/b3A6Njg0NzIxMA-recuperer-une-commande-specifique)

- **Majeur**: Remplacement de la liste `orders` à la racine de la réponse par un objet `order` et réorganisation de celui-ci. 
A noter que c'est la dernière commande connue avec cet identifiant qui est retournée.

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      "picking": {
        ...
      },
      "delivery": {
        ...
      },
      "order": {
        "id": "A1234",
        "referenceNumber": "A6172"
      }
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "order":
  {
    "id": "A1234",
    "referenceNumber": "A6172",
    "picking": {
      ...
    },
    "delivery": {
      ...
    }
  }
}
```
<!-- type: tab-end -->


- **Majeur**: Remplacement du champs `currentStatus` par deux champs `status` et `subStatus` dans `delivery`: [Explication des nouveaux status de livraisons](https://api.woopit.fr/docs/retailer/ZG9jOjEwMDkzODc-statuts-de-livraison)

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      ...,
      "delivery": {
        "currentStatus": "DELIVERY_FAILED_WITH_RETURN"
      }
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "order":
  {
    ...,
    "delivery": {
      "status": "DELIVERY_KO",
      "subStatus": "FAILED_WITH_RETURN"
    }
  }
}
```
<!-- type: tab-end -->


- **Majeur**: Remplacement du champs `currentStatus` par un champs `status` dans `order`:

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      ...,
      "order": {
        "id": "AZTT5456",
        "currentStatus": "ORDER_DELIVERED"
      }
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "order": {
    "id": "AZTT5456",
    "status": "ORDER_DELIVERED",
    ...
  }
}
```
<!-- type: tab-end -->


- **Majeur**: Ajout de `parcels` et déplacement des infos `packages` dans celui-ci. Le `currentStatus` est déplacé au niveau de `parcels` et `currentStatus` deviens `status` et `subStatus`:
A noter que pour un `package` reçu dans le POST /orders le transporteur crée un `parcel`.

<!--
type: tab
title: 1.5
-->
```json
{
  "orders": [
    {
      ...,
      "order": {
        "id": "ETHJU6",
        ...
      },
      "packages": [
        {
          "id": "1324",
          "reference": "B8413DD",
          "currentStatus": "DELIVERY_DELIVERED_OK",
          "products": [
            {
              "type": "TYPOLOGY_GENERIC",
              "ean": "4dq86zd4q6zd4q64",
              "cug": "q56zd4q65d4q",
              "label": "Lampe",
              "quantity": 1
            }
          ],
          "quantity": 1
        }
      ]
    }
  ]
}
```

<!--
type: tab
title: 1.6
-->
```json
{
  "order": {
    "id": "ETHJU6",
    "parcels": [{
      "id": "56f74d65s4f564ds6",
      "trackingId": "77899656544BY",
      "status": "DELIVERY_KO",
      "subStatus": "FAILED_WITH_RETURN",
      "barcode": {
        "value": "7841122236655",
        "type": "barcode",
        "format": "128"
      },
      "package": {
        "id": "1324",
        "reference": "B8413DD",
        "products": [
          {
            "type": "TYPOLOGY_GENERIC",
            "ean": "4dq86zd4q6zd4q64",
            "cug": "q56zd4q65d4q",
            "label": "Lampe",
            "quantity": 1
          }
        ]
      }
    }],
    ...
  }
}
```
<!-- type: tab-end -->

## Woop vers Enseignes

### 1.5 -> 1.6

#### PUT /carrier
[Lien vers la documentation](https://api.woopit.fr/docs/retailer/b3A6MTAwODE5NQ-recevoir-le-nom-du-transporteur-selectionne-pour-une-commande)

- **Mineur**: Ajout des informations des `parcels`

```json
{
  ...,
  "parcels": [{
    "id": "56f74d65s4f564ds6",
    "trackingId": "77899656544BY",
    "status": "DELIVERY_KO",
    "subStatus": "FAILED_WITH_RETURN",
    "barcode": {
      "value": "7841122236655",
      "type": "barcode",
      "format": "128"
    },
    "package": {
      "id": "1324",
      "reference": "B8413DD",
      "products": [
        {
          "type": "TYPOLOGY_GENERIC",
          "ean": "4dq86zd4q6zd4q64",
          "cug": "q56zd4q65d4q",
          "label": "Lampe",
          "quantity": 1
        }
      ]
    }
  }]
}
```
