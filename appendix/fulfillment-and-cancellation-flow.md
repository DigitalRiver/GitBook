---
description: This page contains additional helpful information about Fulfillments.
---

# Fulfillment and cancellation flow

## Understanding fulfillment flow

When a cart is successfully submitted, an order is created in both Salesforce and Digital River. On the Digital River end, an order has a defined lifecycle with different stages. An event is created in Digital River when the order goes to a different stage in its lifecycle.

Whenever a Digital River Order is created, and the payment has been authorized (passed fraud check), then the `order.accepted` event is created. This event triggers the fulfillment flow between Salesforce and Digital River. Currently, the Digital River App supports fulfillments at the line-item level except for cancellations which can be done at both the order and line-item level.

## Fulfillment flow

The following sequence diagram outlines the flow during fulfillment.

![](<../.gitbook/assets/Fulfillment\_Flow\_Phase-2.0 (1) (1).png>)

The following list shows the sequence of steps in the fulfillment flow:

1. On successful Digital River order creation and payment authorization, an `order.accepted` event is created at the Digital River end.
   * This will send a notification to Salesforce by making a call to the following registered webhook endpoint exposed through this app: \
     `<>/services/apexrest/digitalriverv2/ DROFIOrderMgmNotification/`
   * This notification has all the relevant information like the type of event and the data associated with the event.
   * The app creates a Digital River fulfillment record in Salesforce with the Digital River order identifier. **OFI Received** flag on this record will be set to `TRUE`.
   * Clients should start their fulfillment process only after the OFI Received flag is checked on the Digital River fulfillment record for the order as this indicates that Digital River was able to authorize the payment and it has passed the fraud check.
2. Whenever a line item is fulfilled at the client-side, they need to update the Digital River Order Item State field on CC Order Item to **fulfilled**.
   * This will create a Digital River Line Item Fulfillment Record for this line item.
   * The Digital River Line Item Fulfillment Record will have all the relevant information like CC Order Item Id, Digital River Line Item ID, Line Item Quantity, Parent Digital River Fulfillment Record Id, and other information required to send fulfillment information to Digital River. Currently, the app does not support partial fulfillment.
   * **EFN OrderItem Status** field will be **Open** when this record is initially created.
   * The fulfillment job runs on a schedule and picks up all Digital River Line Item Fulfillment records whose **EFN OrderItem Status** is either **Open** or **Pending**.
     * EFN OrderItem Status will be set to Pending if there is a failure while sending fulfillment information to Digital River.
     * EFN OrderItem Status will be set to `Completed` when the fulfillment information is successfully sent to Digital River.
3. Digital River Order will be moved to `Completed` state, when fulfillment information is sent for all the line items in that order and funds are captured.
   * This will create an `order.complete` event at the Digital River end.
   * On creation of this event, a notification will be sent to the following registered webhook endpoint: \
     `<>/services/apexrest/digitalriverv2/ DROrderCompleteNotification/`
   * The app sets the **OCN Received** flag on the Digital River Fulfillment record to `true`.
   * The **Digital River Order state** field on CC Order is updated to **complete**.

{% hint style="info" %}
**Note:** See [Step 9: Set up webhooks](../integrating-the-digital-river-salesforce-b2b-commerce-app/step-9-set-up-webhooks.md) for instructions on registering a Webhook URL.
{% endhint %}

## Cancellation flow between Salesforce and Digital River

You can request a cancellation at the order as well as at the line-item level. However, you can only cancel at the order level when none of the line items in the order are previously fulfilled. The following list explains the conditions when you can cancel a CC Order:

* The Digital River Order State on CC Order is `accepted` or `pending_payment` or `in_review` or `blocked.`
* The Digital River Order Item state on CC Order Items is either `created` or `cancelled.`

{% hint style="info" %}
If the above conditions are not satisfied, then an error will occur when trying to cancel the CC order.
{% endhint %}

## Order-level cancellation flow

The following list shows the sequence of steps between Salesforce and Digital River during an order-level cancellation:

1. Set the **Digital River Order State** field on CC Order to `cancelled`.
2. The CC Order Trigger in the Digital River App will update the **Digital River Order State** field on the Digital River Fulfillment record for this Order to `cancelled`.
3. The Order Level Fulfillment job runs on a schedule and picks up all Digital River fulfillment records whose **EFN Status** is `Open` or `Pending` and **Digital River Order State** is `cancelled`.
4. The Order Level Fulfillment job will take care of sending cancellation requests for all the line items in the order.
5. The **EFN Status** on the Digital River Fulfillment record will be updated to `Completed` once the cancellation information is successfully sent to Digital River.
6. The **OCN Received** flag on the Digital River Fulfillment record will not be updated to `true` for order-level cancellations.

## Line-item level cancellation flow <a href="#line-item-level-cancellation-flow" id="line-item-level-cancellation-flow"></a>

This flow is exactly similar to the steps mentioned in the [Fulfillment flow](../integrating-the-digital-river-salesforce-b2b-commerce-app/step-8-set-up-digital-river-fulfillments.md#fulfillment-flow). The only difference is in Step 2 where you need to update the **Digital River Order Item State** field on the CC Order Item to `cancelled` instead of `fulfilled`. The remainder of the flow will remain the same.

{% hint style="info" %}
For order-level cancellation, you should only set the **Digital River Order State** field on CC Order to `cancelled`. The **Digital River Order Item State** field on **CC Order Items** should be set to `cancelled` only when you create a line-item level cancellation.
{% endhint %}
