# Booking status 

During its life cycle, a booking goes through several :

- order booking

### List of possible booking statuses

| Status                            |Sub Status                    | Title                    | Description                                                                |
| --------------------------------- | ------------------------| ------------------------ | -------------------------------------------------------------------------- |
| `PICK_UP_POINT_BOOKING_INIT`                   | | Booking init         | The booking has been successfully created.                        |
| `PICK_UP_POINT_BOOKING_OK`                   | | Booking registered         | The booking has been successfully registered.                        |
| `PICK_UP_POINT_BOOKING_KO`                   | | Error booking | The pick-up point booking failed.                        |
| `PICK_UP_POINT_BOOKING_CANCELLED`                  | | Booking cancelled         | The booking has been cancelled.                         |
| `PICK_UP_POINT_LOADING_OK`                   | | Loading ok         | The parcel has been dropped at the pick-up point.                        |
| `PICK_UP_POINT_LOADING_KO`                   | | Error loading        | An error occurred when trying to drop the parcel at the pick-up point                |
| `PICK_UP_POINT_LOADING_KO`                   |`FULL`| Error loading        | Impossible to drop the parcel at the pick-up point because this one is full                |
| `PICK_UP_POINT_COLLECTION_OK`                   | | Collection ok         | Collection performed by the final customer.                        |
| `PICK_UP_POINT_COLLECTION_OK`                  |`MANUAL` | Collection ok - manuel         | Collection ok with the manual mode.                        |
| `PICK_UP_POINT_COLLECTION_OK`               |`EXPIRED`  | Collection ok - expired         | Collection ok when the parcel is expired .                        |
| `PICK_UP_POINT_COLLECTION_KO`                |`FAILED` | Error collection         | An error occurred when the receiver tried to collect the parcel.                       |
| `PICK_UP_POINT_COLLECTION_KO`                |`BLOCKED` | Error collection         | The collection has been blocked by the retailer.                        |
| `PICK_UP_POINT_COLLECTION_KO`                |`NOT_COLLECTED` | Error collection         | The parcel has not been collected on time by the final customer.                        |

### Link between order, delivery and booking status

![SPIDER - Workflow statuts-__ status  (1).jpg](<../../../assets/images/SPIDER - Workflow statuts-__ status  (1).jpg>)



