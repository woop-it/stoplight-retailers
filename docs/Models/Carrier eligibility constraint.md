# Carrier eligibility constraint 

Each carrier has a set of delivery and/or picking constraints. WOOP allows these carriers to register their constraints and to operate the requests according.

Let's note here some of these constraints: 

Code | Title
---------|----------
 `delivery.promise`| Promise of delivery for the carrier
 `DurationSlot`| Delivery duration defined by slot
 `delivery.noticePeriod`| Notice period required to take delivery
 `delivery.minDeliveryTime`| Minimum duration expressed by the carrier

### Delivery promise 

Expressed in days or hours, the delivery promise defines the time allowed by the carrier to deliver. After this time, we can consider that the carrier does not respect its promise and the initial delivery commitment. 

**> Example** `delivery.promise` = 48 hours. Delivery must be made within the next 48 hours.

### Duration slot 

The duration of each delivery slot from the following choices: 1/2h, 1h, 2h, 4h or all day. 

**> Example** `durationSlot` = 2 hours. Delivery is made in 2 hour slots.

### Notice period 

Expressed in days or hours, the notice period is used to secure the handling of an order for the carrier. This period defines the necessary notice time defined for the carrier to authorise the taking over of a given order. If this time is not respected and the request is made 'out of time' the carrier cannot take charge of the request. 

**> Example** `delivery.noticePeriod` = 4 hours. The carrier must be notified 4 hours before the actual picking date.

### Min delivery time 

Expressed in days or hours, the minimum delivery time is used to define the first possible delivery date for the carrier. This period defines the time needed for the carrier to deliver the order (1st deadline). Note here that the carrier is committed to delivering the order from the `delivery.minDeliveryTime` to the `delivery.promise`.

**> Example** `delivery.minDeliveryTime` = 24 hours. **Subject to the other constraints defined**, first carrier delivery slot within 24 hours.*
