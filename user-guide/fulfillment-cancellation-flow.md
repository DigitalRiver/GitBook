---
description: Learn more about the fulfillment/cancellation flow.
---

# Fulfillment/cancellation flow

## Fulfillment/cancellation model&#x20;

In this model, listen for the `order.accepted` event before initiating the fulfillment/cancellation process.

There are two ways to do fulfillments/cancellations:

* Order level fulfillment/cancellation
* Line level fulfillment/cancellation

### Fulfillment/cancellation flow sequence diagram

{% file src="../.gitbook/assets/DR-Fulfillment-Flow-Support-Batch-Partial.png" %}

### Order level fulfillment/cancellation&#x20;

You can initiate an Order level fulfillment/cancellation request to Digital River by changing/updating the **Digital River Order State** field on a specific order as follows:

* For Order level fulfillment, change the **Digital River Order State** field on the order to `fulfilled`.
* For Order level cancellation, change the **Digital River Order State** field on the order to `cancelled`.

Changing the **DR Order State** field value to either `fulfilled` or `cancelled` on an order will result in the following:

* Triggers the creation of `DR Fulfillment Request Log` records corresponding to each order item in the Order that has not been previously fulfilled or cancelled. The Fulfillment/Cancel Quantity on the Fulfillment Request Log records will be set equal to the DR Open Quantity value on the Order Item.
* Updates the relevant fields on the `Digital River Fulfillment` object with Digital River and Salesforce order-related information (for example, **Digital River Order State**).
* Creates corresponding `DR Line Item Fulfillment` records for each order line item that has not previously been fulfilled or cancelled.
* The Fulfillment/Cancellation batch job run transmits relevant line item fulfillment/cancellation requests on a given order to Digital River on its next scheduled.
* Once Digital River processes the relevant line-item fulfillment/cancellation requests successfully for an order, the **Digital River Fulfillment Status** field is set to **complete** on both:
  * The `Digital River Fulfillment` object for the order
  * The `DR Line Item Fulfillment` objects for the order

### Line item level fulfillment/cancellation

A line item level fulfillment/cancellation request to Digital River can be initiated by creating the relevant `DR Fulfillment Request Log` record for the line-item level record. See the [DR Fulfillment Request Log object ](fulfillment-cancellation-flow.md#dr-fulfillment-request-log-object)for details on this record.

* You can create the `DR Fulfillment Request Log` record for the line-item level record by populating the Salesforce Order Number, Salesforce Order Item Id, Fulfillment Quantity, and Cancel Quantity fields. The Digital River app populates all the other fields automatically.
* You can initiate complete line-item fulfillment by setting the Fulfill Quantity to the Full Quantity of the Line Item. Similarly,  you can initiate complete line-item cancellation by setting the Cancel Quantity to the Full Quantity of the line item.
* You can initiate partial line-item fulfillment by setting the Fulfill Quantity to a number less than the Full Quantity of the line item. Similarly, you can initiate partial line-item cancellation by setting the Cancel Quantity to a number less than the Full Quantity of the line item.
* You can create the DR Fulfillment Request Log record by setting both Fulfill Quantity and Cancel Quantity for a line item in a single request. The sum of the fulfill quantity and cancel quantity must be less than or equal to the DR Open Quantity field on the line-item record.
* When the system creates fulfillment/cancellation request log records, it also creates the corresponding line item level requests in Digital River Line Item Fulfillments for each of the fulfilled/cancelled order line-item records (for both partially and completely fulfilled/cancelled line items). You can either completely fulfill or cancelled each line item (for example, your Line item Qty = 10 and you fulfill 10) or partially fulfill or cancel some of the line items (for example, your Line item Qty = 10, and you fulfill 5).&#x20;
* The Fulfillment/Cancellation batch job transmits relevant line-item fulfillment/cancellation requests for an order to Digital River on its next scheduled run.
* Once Digital River processes the relevant line-item fulfillment/cancellation requests successfully for an order, the system sets the **Digital River Fulfillment Status** field to `completed` on the relevant DR Line Item Fulfillment objects for the order.
* The system does not set the **Digital River Fulfillment Status** field to `completed` in Digital River Fulfillment until all the line items are fulfilled/cancelled. Until then, the status will remain `open`.
* When the Fulfillment/Cancellation batch job finishes, the Digital River Order Item state on the relevant OrderItem records will be set to one of the following states:
  * `Fulfilled`–If the DR Fulfilled Quantity is greater than zero and equal to the Purchased OrderItem Quantity.
  * `partially_fulfilled`–If the DR Fulfilled Quantity is greater than zero and less than the Purchased OrderItem Quantity.
  * `cancelled`–If the DR Cancelled Quantity is greater than zero and equal to the Purchased OrderItem Quantity.
  * `partially_cancelled`–If the DR Cancelled Quantity is greater than zero and less than the Purchased OrderItem Quantity.

{% hint style="info" %}
The sum of the fulfill quantity or cancel quantity on the DR Fulfillment Request Log record must always be less than or equal to the DR Open Quantity value on the OrderItem record
{% endhint %}

### Fulfillment/cancellation batch job&#x20;

When the scheduled `digitalriverv3.DRB2B_OrderFulfillmentBatchJob`runs, it transmits relevant line-item level fulfillment/cancellation requests (pertaining to both Order level and Line-item level fulfillment/cancellation requests) to Digital River.

## Custom fulfillment/cancellation objects&#x20;

The following custom objects are part of the fulfillment/cancellation process:

* DR Fulfillment Request Log
* Digital River Fulfillment
* DR Line Item Fulfillment

### DR Fulfillment Request Log object&#x20;

Custom `DR Fulfillment Request Log` object is used to store Fulfillment/Cancellation requests related transaction logs information from the client application for Order level or Line-item level fulfillment/cancellation requests.

A `DR Fulfillment Request Log` record should be created (either manually or through automation) whenever an order or order line item is fulfilled/cancelled on the client side.

The `DR Fulfillment Request Log` custom object has the following custom fields in it:

| Field label      | Description                              |
| ---------------- | ---------------------------------------- |
| Order Id         | Salesforce Order Id                      |
| Order Item Id    | Salesforce Order Item Id                 |
| Fulfill Quantity | Specifies Order item quantity to fulfill |
| Cancel Quantity  | Specifies Order item quantity to cancel  |
| DR Order Id      | The Digital River Order Id               |
| DR Order State   | The state of the Digital River order     |
| DR OrderItem Id  | The Digital River Order Item Id          |

The DR Fulfillment Request Log record (fulfillment/cancellation request) creation requires the following fields to be populated:

* Order Id
* OrderItem Id
* Fulfill Quantity&#x20;
* Cancel Quantity

![](<../.gitbook/assets/DR fulfillment requst log object.png>)

### Digital River Line Item Fulfillments and Digital River Fulfillment objects

* When a DR Fulfillment Request Log record is created for fulfillment/cancellation request, corresponding line-level fulfillment/cancellation requests are automatically created in Digital River Line Item Fulfillments.
* When Salesforce receives an `order.accepted` event for an order, a corresponding Order level Fulfillment record is created in the `Digital River Fulfillment` object.
* When a fulfillment occurs at the order level, a corresponding DR Line Item Fulfillment object is automatically created for each line item that has not previously been fulfilled or cancelled.
* When a line item is fulfilled/cancelled, a corresponding DR Line Item Fulfillment object is automatically created.

#### Digital River Fulfillment object

This object contains the Order Level Fulfillment/Cancellation information.

| Field label                            | Description                                                                                                                                              |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Digital River Fulfillment Status       | Represents `DR Order Fulfillment` status. Valid values are Open, Reprocess, Completed, and Failed                                                        |
| Digital River Order Id                 | The Digital River order identifier                                                                                                                       |
| Digital River Order State              | The state of the Digital River order                                                                                                                     |
| Eligible For Fulfillment               | Indicates if the Order is eligible for Fulfillment. This will be set to `true` when an `order.accepted` event is received by Salesforce.                 |
| Is Fulfillment Completed               | Indicates if the Fulfillment process is completed. This will be set to true when an `order.complete` event is received by Salesforce.                    |
| Order Cancelled                        | Indicates if the Order has a cancelled state within Digital River.  This will be set to true when the order.cancelled event is received by Salesforce.   |
| Message                                | Text Field to capture debug information                                                                                                                  |
| Order Id                               | Salesforce Order Id                                                                                                                                      |
| Retry Attempts Made                    | Number of Attempts made for posting Fulfillment information to DR                                                                                        |
| Number Of Line Item Records to Process | count of Child Line Item Fulfillment Records available for Fulfillment or Cancellation (that is, Fulfillment Order Item Status is `Open` or `Reprocess`) |

![](<../.gitbook/assets/DR Fulfillment object.png>)

#### DR Line Item Fulfillment object&#x20;

This object has custom fields to capture Order Item Fulfill and Cancel quantities requested by the client. This information will be posted to DR as part of the fulfillment/cancellation request:

| Field label                     | Description                                                                                                                      |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Fulfill Quantity                | Specifies Order Item Quantity to Cancel                                                                                          |
| Cancel Quantity                 | Specifies Order Item Quantity to Fulfill                                                                                         |
| SF Order Item                   | Salesforce Order Item Id                                                                                                         |
| DR OrderItem Id                 | Digital River Order Item Id                                                                                                      |
| Digital River Order Fulfillment | Specifies the Order Level Fulfillment Record                                                                                     |
| DR Fulfillment Request Log      | Specifies the DR Fulfillment Request Log Record                                                                                  |
| Fulfillment OrderItem Status    | Represents the Digital River Order Item Fulfillment status. The valid values are `Open`, `Reprocess`, `Completed`, and `Failed`. |
| Message                         | Provide information on the success or failure when posting fulfillment to Digital River.                                         |
| Retry Attempts Made             | Number of retry attempts when sending Line Level Fulfillment information to Digital River.                                       |

### Order item object&#x20;

Custom fields have been created on the `Order Item` object to store the following items for an order line item:

| Field label                    | Description                                                                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| DR Open Quantity               | Line-Item Quantity Available for Fulfillment or Cancellation                                                                   |
| DR Fulfilled Quantity          | Fulfilled Line-Item Quantity                                                                                                   |
| DR Cancelled Quantity          | Cancelled Line-Item Quantity                                                                                                   |
| Digital River Order Item State | Represents DR Order Item States. Valid values are created, fulfilled, cancelled, partially\_fulfilled and partially\_cancelled |

Once the order has been created, the **DR Open Quantity** field on the `Order Item` object will be updated and set to the **actual purchased quantity**.

Once a successful response is received from DR for fulfillment/cancellation requests, the **Digital River Order Item State** and **DR Fulfilled Quantity/DR Canceled Quantity** are updated on the `Order Item` object.

Once a fulfillment/cancellation request for a particular order line item is successfully processed by Digital River, the **DR Order Item State** field will be set to **fulfilled/cancelled** and the **DR Fulfilled Quantity/DR Canceled Quantity** to the quantity in fulfillment/cancellation request respectively.

The **DR Open Quantity** field will be updated once `DR Fulfillment Request Log` record is created. This will be changed to zero so that no future requests are made for already fulfilled/cancelled line items.

The following screenshots show an Order Item before it is fulfilled/cancelled:

![](<../.gitbook/assets/Order item fulfillment 1.png>)

![](<../.gitbook/assets/Order item fulfillment 2.png>)

The following screenshot shows an Order Item after it is fulfilled/cancelled:

![](<../.gitbook/assets/Order item fulfillment 3.png>)

## Fulfillment/cancellation batch flow

The Salesforce Lightning app comes with the ability to batch Fulfillments/Cancellations Line Item requests. You can enable the ability to batch Fulfillment/Cancellations Line Item requests and define the wait time interval when you [configure the fulfillment/cancellation settings](../integrate-the-salesforce-lightning-app/step-2-configure-the-digital-river-app.md#configure-the-fulfillment-cancellation-settings).  The wait time interval defines how long the app will wait after the first fulfillment/cancellation request before sending all pending requests for that order to Digital River.  NOTE: The interval does not affect the [schedule](../integrate-the-salesforce-lightning-app/step-9-schedule-backend-jobs.md) of the fulfillment batch job.

The following list shows the fulfillment/cancellation batch flow.

1. Fulfillment/cancellation batch job will pull in all DR Order Fulfillment records when:
   1. The **DR Fulfillment Status** is either `Open` or `Reprocess`.
   2. **Eligible for Fulfillment** is `true`. That is, the system received the `order.accepted` event.
   3. There are **Child DR Line Item Fulfillment** records in the `Open` or `Reprocess` states.
2. Process each DR Order Fulfillment record.
   1. If the corresponding Order is completely fulfilled/cancelled (that is., the DR Open quantity field on all the line items is 0), then the relevant line-item level fulfillment/cancellation requests (on both Order level and Line-Item level fulfillment/cancellation requests) are sent to Digital River.
   2. If you [set **Batch Fulfillments** configuration to **true**](../integrate-the-salesforce-lightning-app/step-2-configure-the-digital-river-app.md#configure-the-fulfillment-cancellation-settings), then:
      * The system will batch all the Open DR line Item fulfillment requests as a single request.
      * The connector will wait for the specified time interval (in minutes) after the system receives the first line item fulfillment request for an Order.
      * If the difference between the earliest created DR Line Item Fulfillment record (with an Open or Reprocess status) corresponding to the DR Fulfillment record and the configured time is greater than 0 by the time the batch job runs, then all Line Item fulfillment/cancellation requests received for this Order will be batched together into a single request and sent to Digital River.
   3. If you [set **Batch Fulfillments** to **false**](../integrate-the-salesforce-lightning-app/step-2-configure-the-digital-river-app.md#configure-the-fulfillment-cancellation-settings), then all line item fulfillment cancellation requests (with an open or Reprocess status) received for this Order will be sent to Digital River at the time the scheduled job runs.

