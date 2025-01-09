---
stoplight-id: 4b8m2u93fss6p
---

# Changelog 1.8 -> 1.9

All changes between version 1.8 and version 1.9 are listed here.

## POST /orders et PATCH /orders/{orderId}

- Section `carrierSelection` added to enable the retailer to include or exclude a list of carriers from the orchestration. This section is composed by a `mode` (INCLUSION or EXCLUSION) and a list of `carrierCodes`. If mode = INCLUSION, then only the carriers from the list will be involved in the process. If mode = EXCLUSION, then the carriers from the list will be excluded from the process.

## PUT /orders/{orderId}/trackings

- This new callback allows the Retailer to receive the tracking page url when the carrier send it to Woop

## Woop to retailer

- The vehicleType model has been modified within the `/orders/{orderId}/carrier`, `/orders/{orderId}/stops` and `/orders/{orderId}/quotes` methods.

## Retailer to Woop

- The vehicleType model has been modified within the `/orders/{orderId}` method.