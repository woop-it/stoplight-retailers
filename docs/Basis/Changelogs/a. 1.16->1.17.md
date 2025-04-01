---
tags: [changelog]
stoplight-id: b2op1wdi8y32c
---

# Changelog 1.16 -> 1.17

Changes between version 1.16 and version 1.17 are listed here.

## Promise

### Addition of the New Promise Calculation in postEligibilities

The new promise calculation in the postEligibilities endpoint is universal and applies to all versions of the API without exception.
In version 1.17.0, the response format has evolved. The difference between versions prior to 1.17.0 and this version lies in a change in the response format. For versions below 1.17.0, there were separate fields for minPickingDate and minDeliveryDate. In version 1.17.0, these fields are replaced with a promises object that includes picking and delivery intervals, as well as values for DP, DML, and cutOffs.

### Addition of the New Promise Calculation in postOrders

The behavior of the calculation in the postOrders endpoint varies depending on the API version used.
Starting with version 1.17.0, no intervals are mandatory. If no parameters are provided by the user, an empty call is made, allowing the evaluation of available slots based on default data.

## Dangerous goods
