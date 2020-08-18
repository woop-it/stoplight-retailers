# Modèles

### Location
Un emplacement représente un lieu de prélevement ou de livraison, trois types d'emplacement sont disponibles :


<!--
type: tab
title: Adresse
-->

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

```json
{
  "type": "exchangePlace",
  "id": "1"
}
````
<!-- type: tab-end -->


