---
description: Learn how notifications trigger status updates.
---

# Status mappings

Status mappings provide a comprehensive view of how orders transition through various stages from inception to completion. Understanding these mappings is crucial for interpreting the status updates received from Digital River and their corresponding statuses in BigCommerce. This section details the specific status changes for different types of orders, ensuring clarity and accuracy in tracking an order’s lifecycle.

## Order with a physical product only

An order that contains only a physical product typically follows a standard workflow involving multiple statuses for payment and fulfillment. The table below illustrates the different statuses an order can have from the initial notification received from Digital River through to the completed order status in BigCommerce and Digital River systems.

<table><thead><tr><th>Notification received from Digital River</th><th width="200">BigCommerce payment status</th><th>BigCommerce order status</th><th>Digital River order status</th></tr></thead><tbody><tr><td>none</td><td>Pending</td><td>Pending</td><td>pending_payment</td></tr><tr><td>none</td><td>Pending</td><td>Awaiting Payment</td><td>pending_payment</td></tr><tr><td>order.accepted</td><td>Authorized</td><td>Awaiting Payment</td><td>accepted</td></tr><tr><td>none</td><td>Authorized</td><td>Shipped</td><td>fulfilled</td></tr><tr><td>order.charge.capture.complete</td><td>Pending</td><td>Shipped</td><td>complete</td></tr></tbody></table>

## Order with a digital product only

An order containing only a digital product involves a more streamlined workflow compared to physical products, primarily focusing on payment authorization and fulfillment. The table below outlines the various statuses such an order can transition through, from the initial notification received from Digital River to the final completed order status in both BigCommerce and Digital River systems.

| Notification received from Digital River | BigCommerce payment status | BigCommerce order status | Digital River order status |
| ---------------------------------------- | -------------------------- | ------------------------ | -------------------------- |
| none                                     | Pending                    | Pending                  | pending\_payment           |
| none                                     | Pending                    | Awaiting Payment         | pending\_payment           |
| order.accepted                           | Authorized                 | Awaiting Payment         | accepted                   |
| order.charge.capture.complete            | Captured                   | Awaiting Fulfillment     | fulfilled                  |
| none                                     | Captured                   | Completed                | complete                   |

## Order with mixed products

Orders containing physical and digital products present a more complex workflow than orders with only physical or digital items. The table below describes the various statuses such an order can transition through, detailing how notifications from Digital River synchronize with BigCommerce's payment and order status systems. This ensures that both physical shipments and digital deliveries are accurately tracked and fulfilled.

| Notification received from Digital River | BigCommerce payment status | BigCommerce order status | Digital River order status |
| ---------------------------------------- | -------------------------- | ------------------------ | -------------------------- |
| none                                     | Pending                    | Pending                  | pending\_payment           |
| none                                     | Pending                    | Awaiting Payment         | pending\_payment           |
| order.accepted                           | Authorized                 | Awaiting Payment         | accepted                   |
| none                                     | Authorized                 | Shipped                  | accepted                   |
| order.charge.capture.complete            | Captured                   | Shipped                  | fulfilled                  |
| none                                     | Captured                   | Completed                | complete                   |
