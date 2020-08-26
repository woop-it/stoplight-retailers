# Emplacement 

Un emplacement dit `location` représente un lieu de prélevement ou de livraison physique. Au travers des API, trois types d'emplacement sont disponibles :

<!--
type: tab
title: Adresse
-->
Le type "**address**" représente une addresse postale classique à saisir entièrement lors de la création de commande. Il correspond à l'appel standard le plus classique lors de la création d'une commande. Si l'adresse de prélèvement et/ou de livraison ne sont pas connues, vous avez alors la possibilité d'indiquer en entièrement l'emplacement. 
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
Le type "**pickupPoint**" représente l'emplacement d'un point-relais ou centre de distribution précis d'un transporteur. Il correspond à l'adresse enregistrée pour un transporteur donné associé à ce lieu. Pour utiliser ce type d'emplacement, il est nécessaire de connaitre l'identifiant du point-relais par transporteur.

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
Le type "**exchangePlace**" représente un point de prélévement précis d'un des magasins de l'enseigne. Configuré dans le back-office de Woop, ces informations sont propre au magasin. A la création, vous pouvez définir l'identifiant de votre choix pour chaque point de prélèvement. 

Consulter la page [Point de prélevement (ExchangePlace)](docs/Modèles/ExchangePlace.md)pour plus de détail.
```json
{
  "type": "exchangePlace",
  "id": "1"
}
````
<!-- type: tab-end -->


