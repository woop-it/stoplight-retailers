# Location

A location called `location` represents a physical collection or delivery location. Through the APIs, three types of location are available:

<!--
type: tab
title: Address
-->

The type "**address**" is a standard postal address to be entered in full when creating an order. This is the most common standard call when creating an order. If the collection and/or delivery address is not known, you can indicate the details of the location.

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
title: Relay point
-->

The type "**pickupPoint**represents the location of a specific relay point or a carrier's distribution centre. It corresponds to the address registered for a given carrier at that location. To use this type of location, the identifier of the relay point by carrier is required.

The relay point identifier must be retrieved by [searching for a relay point](https://woop.stoplight.io/docs/retailer/retailer_to_woop.json/paths/~1pickupPoints/get)

```json
{
  "type": "pickupPoint",
  "id": "76761",
  "carrierCode": "bpost"
}
```

<!--
type: tab
title: Collection point
-->

The type "**exchangePlace**" represents a specific collection point in one of the retailer's stores. This information is specific to the store and is configured in the Woop back office. When creating the collection point, you can define the identifier of your choice for each.

View page [Collection point (ExchangePlace)](docs/Modèles/ExchangePlace.md)for more details.

```json
{
  "type": "exchangePlace",
  "id": "1"
}
```

<!-- type: tab-end -->
