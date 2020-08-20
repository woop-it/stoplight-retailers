# Emplacement (Location)

Un emplacement (location) représente un lieu de prélevement ou de livraison, trois types d'emplacement sont disponibles :

<!--
type: tab
title: Adresse
-->
type: "**address**"

Représente une addresse postale classique.
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
title: Point relais
-->
type: "**pickupPoint**"

Représente un point relais précis d'un transporteur.

(Point relais récupéré via [la recherche de point relais](https://woop.stoplight.io/docs/retailer/retailer_to_woop.v1.4.0.json/paths/~1pickupPoints/get))
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
type: "**exchangePlace**"

Représente un point de prélévement de votre enseigne (configuré dans le back-office)
```json
{
  "type": "exchangePlace",
  "id": "1"
}
````
<!-- type: tab-end -->


