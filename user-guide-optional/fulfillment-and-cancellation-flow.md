---
description: Learn more about the fulfillment/cancellation flow.
---

# Fulfillment/cancellation flow

## Fulfillment/cancellation model&#x20;

In this model, listen for the `order.accepted` event before initiating the Fulfillment/cancellation process.

Fulfillments/cancellations are done in two ways:

* Order level fulfillment/cancellation
* Line level fulfillment/cancellation

{% hint style="info" %}
Partial line level fulfillments/cancellations are not supported at this time.
{% endhint %}

### Fulfillment/cancellation flow sequence diagram

{% file src="../.gitbook/assets/DR_FulfillCancel_Flow_V3_1.0.png" %}
Fulfillment/cancellation flow diagram
{% endfile %}

### Order level fulfillment/cancellation&#x20;

An Order Level fulfillment/cancellation request to Digital River can be initiated by changing/updating the **Digital River Order State** field on the order in question as follows:

* For Order level fulfillment, change/update the **Digital River Order State** field on the order to **fulfilled**.
* For Order level cancellation, change/update the **Digital River Order State** field on the order to **cancelled**.

Changing the **DR Order State** field value to either `fulfilled` or `cancelled` on an order will result in the following:

* Triggers the creation of `DR Fulfillment Request Log` record(s) corresponding to each order item in the Order that has not been previously fulfilled or cancelled.
* Relevant fields on `Digital River Fulfillment` object get updated with Digital River and Salesforce order-related information accordingly (for example, **Digital River Order State**).
* Creation of corresponding `DR Line Item Fulfillment` records for each order line item that has not previously been fulfilled or cancelled.
* The Fulfillment/Cancellation batch job on its next scheduled run, transmits relevant line item fulfillment/cancellation requests pertaining to a given order to Digital River.
* Once Digital River processes the relevant line-item fulfillment/cancellation requests successfully for a given order, the **Digital River Fulfillment Status** field is set to **complete** on both (a) `Digital River Fulfillment` object for the order in question and on (b) `DR Line Item Fulfillment` objects for the order.

### Line item level fulfillment/cancellation

A Line Item level fulfillment/cancellation request to Digital River can be initiated by creating the relevant `DR Fulfillment Request Log` record for the line-item level record in question. Refer to the [DR Fulfillment Request Log object ](fulfillment-and-cancellation-flow.md#dr-fulfillment-request-log-object)section for details on this record.

* When fulfillment/cancellation request records are created in `DR Fulfillment Request Log`, corresponding line item level requests are also created in `Digital River Line Item Fulfillments` for each of the order line-item records being fulfilled/cancelled.
* The Fulfillment/Cancellation batch job on its next scheduled run, transmits relevant line-item fulfillment/cancellation requests about a given order to Digital River.
* Once Digital River processes the relevant line-item fulfillment/cancellation requests successfully for a given order, the **Digital River Fulfillment Status** field is set to `completed` on relevant `DR Line Item Fulfillment` objects for the order.
* The **Digital River Fulfillment Status** field will not be updated to `completed` in `Digital River Fulfillment` until all the line items are fulfilled/cancelled. Until then, the status will remain `open`.

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

{% hint style="info" %}
Since Partial Fulfillment/Cancellation **** is not supported at this time, only one of the two fields (Fulfill Quantity or Cancel Quantity) needs to be populated (with the full line item quantity) and the other should be 0.
{% endhint %}

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
| Message                                | Text Field to capture debug information                                                                                                                  |
| Order Id                               | Salesforce Order Id                                                                                                                                      |
| Retry Attempts Made                    | Number of Attempts made for posting Fulfillment information to DR                                                                                        |
| Number Of Line Item Records to Process | count of Child Line Item Fulfillment Records available for Fulfillment or Cancellation (that is, Fulfillment Order Item Status is `Open` or `Reprocess`) |

![](<../.gitbook/assets/DR Fulfillment object.png>)

#### DR Line Item Fulfillment object&#x20;

This object has custom fields to capture Order Item Fulfill and Cancel quantities requested by the client. This information will be posted to DR as part of the fulfillment/cancellation request:

| Field label      | Description                              |
| ---------------- | ---------------------------------------- |
| Fulfill Quantity | Specifies Order Item Quantity to Cancel  |
| Cancel Quantity  | Specifies Order Item Quantity to Fulfill |
| SF Order Item    | Salesforce Order Item Id                 |
| DR OrderItem Id  | Digital River Order Item Id              |

### Order item object&#x20;

Custom fields have been created on the `Order Item` object to store the following items for an order line item:

| Field label           | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| DR Open Quantity      | Line-Item Quantity Available for Fulfillment or Cancellation |
| DR Fulfilled Quantity | Fulfilled Line-Item Quantity                                 |
| DR Cancelled Quantity | Cancelled Line-Item Quantity                                 |

Once the order has been created, the **DR Open Quantity** field on the `Order Item` object will be updated and set to the **actual purchased quantity**.

Once a successful response is received from DR for fulfillment/cancellation requests, the **Digital River Order Item State** and **DR Fulfilled Quantity/DR Canceled Quantity** are updated on the `Order Item` object.

Once a fulfillment/cancellation request for a particular order line item is successfully processed by Digital River, the **DR Order Item State** field will be set to **fulfilled/cancelled** and the **DR Fulfilled Quantity/DR Canceled Quantity** to the quantity in fulfillment/cancellation request respectively.

The **DR Open Quantity** field will be updated once `DR Fulfillment Request Log` record is created. This will be changed to zero so that no future requests are made for already fulfilled/cancelled line items.

The following screenshots show an Order Item before it is fulfilled/cancelled:

![](<../.gitbook/assets/Order item fulfillment 1.png>)

![](<../.gitbook/assets/Order item fulfillment 2.png>)

The following screenshot shows an Order Item after it is fulfilled/cancelled:

![](<../.gitbook/assets/Order item fulfillment 3.png>)

###

###

###
