---
description: Learn how notifications trigger status updates.
---

# Status mappings

## Order with a physical product only

| Notification received from Digital River | BigCommerce payment status | BigCommerce order status | Digital River order status |
| ---------------------------------------- | -------------------------- | ------------------------ | -------------------------- |
| none                                     | Pending                    | Pending                  | pending\_payment           |
| none                                     | Pending                    | Awaiting Payment         | pending\_payment           |
| order.accepted                           | Authorized                 | Awaiting Payment         | accepted                   |
| none                                     | Authorized                 | Shipped                  | fulfilled                  |
| order.charge.capture.complete            | Pending                    | Shipped                  | complete                   |

## Order with a digital product only

| Notification received from Digital River | BigCommerce payment status | BigCommerce order status | Digital River order status |
| ---------------------------------------- | -------------------------- | ------------------------ | -------------------------- |
| none                                     | Pending                    | Pending                  | pending\_payment           |
| none                                     | Pending                    | Awaiting Payment         | pending\_payment           |
| order.accepted                           | Authorized                 | Awaiting Payment         | accepted                   |
| order.charge.capture.complete            | Captured                   | Awaiting Fulfillment     | fulfilled                  |
| none                                     | Captured                   | Completed                | complete                   |

## Order with mixed products

| Notification received from Digital River | BigCommerce payment status | BigCommerce order status | Digital River order status |
| ---------------------------------------- | -------------------------- | ------------------------ | -------------------------- |
| none                                     | Pending                    | Pending                  | pending\_payment           |
| none                                     | Pending                    | Awaiting Payment         | pending\_payment           |
| order.accepted                           | Authorized                 | Awaiting Payment         | accepted                   |
| none                                     | Authorized                 | Shipped                  | accepted                   |
| order.charge.capture.complete            | Captured                   | Shipped                  | fulfilled                  |
| none                                     | Captured                   | Completed                | complete                   |
