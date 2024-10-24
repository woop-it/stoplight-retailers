---
tags: [changelog]
stoplight-id: 0gchp6x2folkj
---

# Changelog 1.15 -> 1.16

Changes between version 1.15 and version 1.16 are listed here.

## Order states

### Add new item in list of possible order states

New order.state = ORDER_WITHOUT_SHIPMENT 

| States                  | Title                                                        |
| ----------------------- | ------------------------------------------------------------ |
| `ORDER_TO_BE_COMPLETED` | Order awaiting further information. Request to be completed. |
| `ORDER_WITHOUT_SHIPMENT` | Order without carrier charter. Orders in this status are received with delivery information only.|

## POST /orders input

### Improvement to the order.state component

When declaring an order, it will now be possible to send additional information depending on the status of the order (order.state). 

The general idea is to provide information specific to the delivery in the creation request for state = ORDER_WITHOUT_SHIPMENT. 

<!--
type: tab
title: Versions up to 1.15.0
-->

```json
{
  "state": "ORDER_TO_BE_COMPLETED"
}
```
<!--
type: tab
title: From version 1.16.0
-->
```json
{
  "code": "ORDER_WITHOUT_SHIPMENT",
  "options": {
    "deliveryId": "A234D4F",
    "parcelIds": [
      "12345",
      "94554J"
    ]
  }
}
```
<!-- type: tab-end -->

This information will be used for the tracking of the delivery. 

## POST /deliveryPromise

### New API to determine the delivery promise

Add new API for calculating the delivery promise, taking account of carrier constraints.

This method can calculate the delivery promise with or without picking and delivery intervals.

<!--
type: tab
title: Request example
-->
```json
{
  "orderDate": "2024-01-30T10:00:00",
  "storeId": "string",
  "carrierCodes": [
    "string"
  ],
  "picking": {
    "location": {
      "type": "address",
      "addressLine1": "string",
      "addressLine2": "string",
      "elevator": true,
      "floor": 0,
      "doorCode": "string",
      "postalCode": "59800",
      "city": "LILLE",
      "district": "string",
      "country": "FR",
      "comment": "string",
      "coordinates": {
        "latitude": 0,
        "longitude": 0
      }
    },
    "interval": {
      "start": "2019-12-04T12:30:00+0000",
      "end": "2019-12-04T14:30:00+0000"
    }
  },
  "delivery": {
    "location": {
      "type": "address",
      "addressLine1": "string",
      "addressLine2": "string",
      "elevator": true,
      "floor": 0,
      "doorCode": "string",
      "postalCode": "59800",
      "city": "LILLE",
      "district": "string",
      "country": "FR",
      "comment": "string",
      "coordinates": {
        "latitude": 0,
        "longitude": 0
      }
    },
    "interval": {
      "start": "2019-12-04T12:30:00+0000",
      "end": "2019-12-04T14:30:00+0000"
    }
  }
}
```
<!--
type: tab
title: Response example
-->
```json
{
  "promises": [
    {
      "carrier": {
        "code": "string",
        "name": "string"
      },
      "picking": {
        "interval": {
          "start": "2019-12-04T12:30:00+0000",
          "end": "2019-12-04T14:30:00+0000"
        }
      },
      "delivery": {
        "interval": {
          "start": "2019-12-04T12:30:00+0000",
          "end": "2019-12-04T14:30:00+0000"
        }
      }
    }
  ]
}
```
<!-- type: tab-end -->

## GET /orders/{orderId}/labels/list

### Add packageId field in the response API

This method retrieves a download link for all the package labels in a customer order.

The labels retrieved are either unique or consolidated for the entire order.

<!--
type: tab
title: Versions up to 1.15.0
-->

```json
{
  "labels": [
    {
      "mode": "pdf",
      "size": "A6",
      "url": "https://labels.woopit.fr/XXX"
    }
  ]
}
```
<!--
type: tab
title: From version 1.16.0
-->
```json
{
  "labels": [
    {
      "mode": "pdf",
      "size": "A6",
      "url": "https://labels.woopit.fr/XXX"
      "packageId": "34T5DF"
    }
  ]
}
```
<!-- type: tab-end -->