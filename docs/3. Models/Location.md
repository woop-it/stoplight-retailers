# Location

A location (`location`) represents a picking or delivery place. Through API, 3 location types are available :

<!--
type: tab
title: Address
-->
Type "**address**" represents a postal address to fill entirely during order creation. 
It corresponds to a standard call during order creation. If picking and/or delivery address are not known, you can specify the complete location.
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
Type "**pickupPoint**" represents the location of a pickup point or a ditribution center of a carrier. It corresponds to the address saved for a carrier in association with the pickup point. It is mandatory to have the identifier of the pickup point for the carrier.

The identifier is obtained [by searching the pickup point](https://woop.stoplight.io/docs/retailer/branches/english/retailer_to_woop.v1.4.0.json/paths/~1pickupPoints/get)
```json
{
  "type": "pickupPoint",
  "id": "76761",
  "carrierCode": "bpost"
}
```

<!--
type: tab
title: Exchange place
-->
Type "**exchangePlace**" represents the location of a place associated to a store. The configuration is set in Woop back-office and is specific to the location. The id can be defined on the creation.

Go to the page [Exchange place](https://woop.stoplight.io/docs/retailer/branches/english/docs/3.%20Models/ExchangePlace.md) for more details.
```json
{
  "type": "exchangePlace",
  "id": "1"
}
````
<!-- type: tab-end -->


