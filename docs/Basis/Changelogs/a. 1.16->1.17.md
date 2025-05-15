---
tags: [changelog]
stoplight-id: b2op1wdi8y32c
---

# Changelog 1.16 -> 1.17

Changes between version 1.16 and version 1.17 are listed here.

## Picking and Delivery Promise

### Addition of the New Promise Calculation in postEligibilities

The new promise calculation in the postEligibilities endpoint is universal and applies to all versions of the API without exception.
In version 1.17.0, the response format has evolved. The difference between versions prior to 1.17.0 and this version lies in a change in the response format. For versions below 1.17.0, there were separate fields for minPickingDate and minDeliveryDate. In version 1.17.0, these fields are replaced with a promises object that includes picking and delivery intervals, as well as values for DP, DML, and cutOffs.

### Addition of the New Promise Calculation in postOrders

The behavior of the calculation in the postOrders endpoint varies depending on the API version used.
Starting with version 1.17.0, no intervals are mandatory. If no parameters are provided by the user, an empty call is made, allowing the evaluation of available slots based on default data.

## Create order with 'Dangerous goods'

### Add the fields required in POST /orders 

For deliveries of dangerous goods, additional information is required for shipments from France.

The order creation method now authorizes new fields to correctly define a dangerous product or delivery. 

<!--
type: tab
title: Versions up to 1.16.0
-->

```json
      "products": [
        {
          "type": "TYPOLOGY_GENERIC",
          "ean": "4dq86zd4q6zd4q64",
          "cug": "q56zd4q65d4q",
          "label": "Lampe",
          "quantity": 1
        }
      ],
```
<!-- type: tab-end -->
From version 1.17.0 -> 3 type to declare DANGEROUS goods 
1) TYPOLOGY_DANGEROUS
2) TYPOLOGY_EXCEPTED_QUANTITY
3) TYPOLOGY_LIMITED_QUANTITY


<!--
type: tab
title: DANGEROUS
-->

```json
"products": [
  {
    "type": "TYPOLOGY_DANGEROUS",
    "onu_code": "UN1203",
    "adr_classification": "Class 3",
    "packing_count": 999,
    "packing_type": "Metal drum",
    "description": "string",
    "environmental_risk": true,
    "technical_name": "Flammable solvent",
    "quantity_code": "PBT", 
    "packingCode": "11G"
  }
],
```

<!--
type: tab
title: EXCEPTED_QUANTITY
-->
```json
"products": [
  {
    "type": "TYPOLOGY_EXCEPTED_QUANTITY",
    "packing_count": 999,
    "environmental_risk": true
  }
],
```

<!--
type: tab
title: LIMITED_QUANTITY
-->
```json
"products": [
  {
    "type": "TYPOLOGY_LIMITED_QUANTITY",
    "volume_weight": 15.3,
    "environmental_risk": true
  }
],
```
<!-- type: tab-end -->

## Eligibility method with order's TAG

### Add order TAG to eligibility search

Add order TAGs to a carrier eligibility search. 

<!--
type: tab
title: 1.17.0
-->

```json
        "tags": [
    {
      "key": "string",
      "value": "string"
    }
  ],
```
<!-- type: tab-end -->