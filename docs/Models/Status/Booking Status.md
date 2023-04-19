# Booking status 

During its life cycle, a booking goes through several :

- order booking

### List of possible booking statuses

| Status                            | Title                    | Description                                                                |
| --------------------------------- | ------------------------ | -------------------------------------------------------------------------- |
| `pick_up_point_BOOKING_INIT`                   | Booking init         | The booking has been successfully created by woop.                        |
| `pick_up_point_BOOKING_OK`                   | Booking registered         | The booking has been successfully registered by woop.                        |
| `pick_up_point_BOOKING_KO`                   | Error booking registered registered         | The order has been successfully registered by woop.                        |
| `pick_up_point_BOOKING_CANCELLED`                   | Booking cancelled         |                         |
| `pick_up_point_LOADING_OK`                   | Loading ok         |                         |
| `pick_up_point_LOADING_KO`                   | Error loading        |                 |
| `pick_up_point_COLLECTION_OK`                   | Collection ok         | collection ok by the final customer .                        |
| `pick_up_point_COLLECTION_OK` - `MANUAL`                  | Collection ok - manuel         | collection ok with the manual mode.                        |
| `pick_up_point_COLLECTION_OK` - `EXPIRED`                  | Collection ok - expired         | collection ok when the parcel is expired .                        |
| `pick_up_point_COLLECTION_KO` - `FAILED`                  | Error collection         | error with the parcel collection.                        |

