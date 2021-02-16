# Delivery status

During its life cycle, the order goes through different statuses. Those we identify are the different delivery steps.

### Order workflow

![get-started-icon](../../assets/images/delivery-status-workflow.png)

### List of possible delivery statuses

| Status                           | Label                                
| -------------------------------- | ------------------------------------ 
| `DELIVERY_INIT`                  | Validated by carrier                 
| `DELIVERY_STARTED`               | Courier approching store             
| `DELIVERY_PICK_UP_REACHED`       | Courier arrived to store             
| `DELIVERY_PICK_UP_OK`            | Order picked-up                      
| `DELIVERY_PICK_UP_FAILED`        | Order failed on pick-up              
| `DELIVERY_PICK_UP_PARTIALLY`     | Order partially picked-up            
| `DELIVERY_IN_PROGRESS`           | Order being delivered                
| `DELIVERY_AT_DROP_OF_LOCATION`   | Courier arrived to customer          
| `DELIVERY_DELIVERED_OK`          | Order correctly delivered            
| `DELIVERY_DELIVERED_WITH_CLAIM`  | Order delivered with claims          
| `DELIVERY_DELIVERED_PARTIALLY`   | Order partially delivered            
| `DELIVERY_FAILED_WITH_RETURN`    | Delivery failed with return to store 
| `DELIVERY_RETURNED_TO_PICK_UP`   | Order returned to store              
| `DELIVERY_CANCELLED`             | Delivery cancelled                   
| `DELIVERY_CANCELLED_WITH_RETURN` | Delivery cancelled with return to store 
| `DELIVERY_BLOCKED`               | Delivery is blocked                  
| `DELIVERY_DELAYED`               | Delivery is delayed                  
| `DELIVERY_AVAILABLE`             | Delivery available in pickup point
| `DELIVERY_REPLANNED`             | Delivery date replanned by an appointment with the customer

### Returns and errors handling

![get-started-icon](../../assets/images/product-return-workflow.png)
