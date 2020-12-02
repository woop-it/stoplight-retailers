# Location

A location (`location`) represents a picking or delivery place. Through API, 3 location types are available :

<!--
type: tab
title: Address
-->
Type "**address**" represents a postal address to fill entirely during order creation. 

It corresponds to a standard call during order creation. If picking and/or delivery address aare not known, you can specify the complete place.
```json
{
  "type": "address",
  "addressLine1": "165 avenue de Bretagne",
  "elevator": true,
  "floor": 3,
  "postalCode": "59000",
  "city": "Lille",
  "country": "FR"
}
```
<!--
type: tab
title: Pickup point
-->
Type "**pickupPoint**" represents the location of a pickup point or a carrier ditribution center. It corresponds à l'adresse enregistrée pour un transporteur donné associé à ce lieu. Pour utiliser ce type d'emplacement, il est nécessaire de connaitre l'identifiant du point-relais par transporteur.

L'identifiant du point-relais doit être récupéré par [la recherche de point relais](https://woop.stoplight.io/docs/retailer/retailer_to_woop.v1.4.0.json/paths/~1pickupPoints/get)
```json
{
  "type": "pickupPoint",
  "id": "76761",
  "carrierCode": "bpost"
}
```

<!--
type: tab
title: Point de prélèvement
-->
Le type "**exchangePlace**" représente un point de prélèvement précis d'un des magasins de l'enseigne. Configuré dans le back-office de Woop, ces informations sont propres au magasin. A la création, vous pouvez définir l'identifiant de votre choix pour chaque point de prélèvement. 

Consulter la page [Point de prélevement (ExchangePlace)](docs/Modèles/ExchangePlace.md)pour plus de détails.
```json
{
  "type": "exchangePlace",
  "id": "1"
}
````
<!-- type: tab-end -->


