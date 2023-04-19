# Booking status 

During its life cycle, a booking goes through several :

- order booking

### List of possible booking statuses

| Status                            | Title                    | Description                                                                |
| --------------------------------- | ------------------------ | -------------------------------------------------------------------------- |
| `PICK_UP_POINT_BOOKING_INIT`                   | Booking init         | The booking has been successfully created by woop.                        |
| `PICK_UP_POINT_BOOKING_OK`                   | Booking registered         | The booking has been successfully registered by woop.                        |
| `PICK_UP_POINT_BOOKING_KO`                   | Error booking registered registered         | The order has been successfully registered by woop.                        |
| `PICK_UP_POINT_BOOKING_CANCELLED`                   | Booking cancelled         |                         |
| `PICK_UP_POINT_LOADING_OK`                   | Loading ok         |                         |
| `PICK_UP_POINT_LOADING_KO`                   | Error loading        |                 |
| `PICK_UP_POINT_COLLECTION_OK`                   | Collection ok         | collection ok by the final customer .                        |
| `PICK_UP_POINT_COLLECTION_OK` - `MANUAL`                  | Collection ok - manuel         | collection ok with the manual mode.                        |
| `PICK_UP_POINT_COLLECTION_OK` - `EXPIRED`                  | Collection ok - expired         | collection ok when the parcel is expired .                        |
| `PICK_UP_POINT_COLLECTION_KO` - `FAILED`                  | Error collection         | error with the parcel collection.                        |

