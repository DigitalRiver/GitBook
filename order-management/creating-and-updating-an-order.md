---
description: Learn the basics of processing an order
---

# Processing orders

Once customers are done checking out, how an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is created depends on whether you implement a [Low-code checkout](../integration-options/low-code-checkouts/) or take the [Direct integrations](../integration-options/checkouts/) approach.

If you're using [Direct Integrations](../integration-options/checkouts/), first [convert the checkout to an order](creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) and then handle the[ immediate response](creating-and-updating-an-order.md#processing-the-post-orders-response) and/or [key events that occur early in an order's lifecycle](creating-and-updating-an-order.md#listening-for-and-handling-order-related-webhook-events).

If you're using [Prebuilt Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md), then Digital River handles [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation. You should, however, [configure a webhook(s)](../administration/dashboard/developers/webhooks/) to listen for [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created), [`order.accepted`](events-and-webhooks-1/events-1/event-types.md#order.accepted) and [`order.cancelled`](events-and-webhooks-1/events-1/event-types.md#order.cancelled).

However, no matter which integration option you select, make sure you're set up to process:

* [Events early in an order's lifecycle](creating-and-updating-an-order.md#listening-for-and-handling-order-related-webhook-events).
* [Fulfillment-related events](informing-digital-river-of-a-fulfillment.md#using-fulfillment-related-events)

{% hint style="success" %}
For a list of important [webhook events](events-and-webhooks-1/events-1/) that most integrations should subscribe to, refer to [Key event types](events-and-webhooks-1/events-1/event-types.md).&#x20;
{% endhint %}

## Converting a checkout to an order <a href="#creating-an-order-with-the-checkout-identifier" id="creating-an-order-with-the-checkout-identifier"></a>

With [Direct Integrations](../integration-options/checkouts/), once the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [address](../integration-options/checkouts/creating-checkouts/providing-address-information.md#address-requirements-and-validations) and [payment](../integration-options/checkouts/creating-checkouts/payment-sessions.md#how-to-determine-when-to-create-an-order) requirements are met and customers have reviewed and submitted their order, you should pass `checkoutId` in the body of a [`POST /orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders).

{% tabs %}
{% tab title="POST/orders" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/orders' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "checkoutId": "177452470336"    
}'
```
{% endtab %}
{% endtabs %}

This request primarily serves to authorize payment. Once submitted, your integration should be set up to [process the immediate response](creating-and-updating-an-order.md#processing-the-post-orders-response) as well as [respond to key events](creating-and-updating-an-order.md#listening-for-and-handling-order-related-webhook-events).

You can submit a `POST /orders` whose payload contains `checkoutId` _plus_ additional parameters (provided they adhere to the [request's data contract](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders)). But, when processing the request, Digital River ignores this additional data. So, if you'd like to [update the checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts), you must do so prior to submitting a `POST /orders`.

For example, the following [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `email` address is `johndoe@digitalriver.com`.

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    "id": "856adaff-0176-4bdb-91cb-7304dfd1e7a9",
    ...
    "email": "johndoe@digitalriver.com",
    ...
}
```
{% endtab %}
{% endtabs %}

If you submit a `POST /orders` that contains the checkout's identifier, an updated `email`, and also adds an `upstreamId` that identifies the order in your system, then the response contains a `201 Created` status code. However, `email` is not updated and `upstreamId` is not populated.

{% tabs %}
{% tab title="POST/orders" %}
```
curl --location --request POST 'https://api.digitalriver.com/orders' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "checkoutId": "856adaff-0176-4bdb-91cb-7304dfd1e7a9",
    "email": "janedoe@digitalriver.com",
    "upstreamId": "1J9F17710A6"
}'
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "189917880336",
    ...
    "email": "johndoe@digitalriver.com",
    ...
    "checkoutId": "856adaff-0176-4bdb-91cb-7304dfd1e7a9"
}
```
{% endtab %}
{% endtabs %}

## Handling the `POST /orders` response <a href="#processing-the-post-orders-response" id="processing-the-post-orders-response"></a>

If you're using [Direct Integrations](../integration-options/checkouts/), after you submit a [`POST/orders`](creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) (assuming all upstream [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) requirements have been met), the response will contain a [`409 Conflict`](creating-and-updating-an-order.md#409-conflict) or [`201 Created`](creating-and-updating-an-order.md#201-created) status code.

When handling this immediate response, you need to capture specific data from its payload and use it to update the status of your commerce system. This ensures that downstream fulfillment operations are correctly handled.

### 409 Conflict

![](<../.gitbook/assets/409 Conflict.svg>)

A `409 Conflict` status code indicates that Digital River did not create an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), either due to a payment authorization failure or suspected fraud. The error's `code` and `message` contain more specific information about what triggered the failure.

{% code title="Error" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "failed-request",
            "message": "Failed to charge source."
        }
    ]
}
```
{% endcode %}

Use this error information to update the upstream order's overall status, payment status, and fraud status.

You can also use the error's `message` to inform end customers of the problem. Do not, however, share `code`. Doing so may aid parties that are attempting to carry out fraudulent or malicious activities.

For more details on how to process responses with a `409 Conflict` status code, refer to the [Handling rejected orders](resubmitting-an-order.md) page.

### 201 Created

A `201 Created` status code indicates an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is [`pending_payment`](creating-and-updating-an-order.md#pending-payment), [`in_review`](creating-and-updating-an-order.md#in-review), or [`accepted`](creating-and-updating-an-order.md#accepted).

From the response's payload, retrieve the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `id`, `state`, `fraudState`, and `charges[].state`, and use these values to update the corresponding attributes in the upstream commerce platform's order.

#### Pending payment

![](<../.gitbook/assets/201 Created\_pending\_payment (2).svg>)

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is `pending_payment`, then the fraud review process has been successfully completed but the [payment charge](orders/payment-charges/) is not yet authorized. For more details, refer to [handling pending payment orders](creating-and-updating-an-order.md#handling-pending-payment-orders).

#### In review

![](<../.gitbook/assets/201 Created\_in\_review (2).svg>)

If an [order's ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)`state` is `in_review`, then this indicates that Digital River is conducting a secondary fraud review. For more information, refer to [handling in review orders](creating-and-updating-an-order.md#handling-in-review-orders).

#### Accepted

![](<../.gitbook/assets/201 Created\_accepted.svg>)

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is `accepted`, then the transaction has successfully passed fraud review and the [payment charge](orders/payment-charges/) is authorized. For more information, refer to [handling accepted orders](creating-and-updating-an-order.md#handling-accepted-orders).

## Events early in an order's lifecycle <a href="#listening-for-and-handling-order-related-webhook-events" id="listening-for-and-handling-order-related-webhook-events"></a>

Whether you're using [Drop-in Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md), [Low-code components](../integration-options/low-code-checkouts/implementing-a-components-checkout.md) or [Direct integrations](../integration-options/checkouts/), you'll need to [configure webhooks](../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for some key [events](events-and-webhooks-1/events-1/) that occur early in an [order's lifecycle](orders/the-order-lifecycle.md).

These events notify you of:

* [charge authorization failures](creating-and-updating-an-order.md#the-payment-failure-event)
* [fraud blocks](creating-and-updating-an-order.md#the-fraud-review-failure-event)
* [pending charge authorizations](creating-and-updating-an-order.md#the-pending-payment-event)
* [ongoing fraud reviews](creating-and-updating-an-order.md#the-fraud-review-failure-event-1)
* [accepted orders](creating-and-updating-an-order.md#listening-for-the-order-accepted-event) and
* [cancelled orders](creating-and-updating-an-order.md#the-order-cancelled-event).

Each time you're notified of one of these events, retrieve the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state`, `fraudState`, and `charges[].state` (if available) from its payload, and use this data to update the corresponding attributes in the upstream commerce system's order.

### The charge authorization failure event <a href="#the-payment-failure-event" id="the-payment-failure-event"></a>

![](<../.gitbook/assets/order.charge.failed event.svg>)

An asynchronous [charge authorization](orders/payment-charges/#how-a-charge-is-created) failure triggers an `order.charge.failed` event.

If you receive this event, you can iterate over the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `payment.charges[]` and inspect them for a [failure code or message](orders/payment-charges/#handling-failures). The `failureMessage` however is not always available. But when it is, you can use it to provide more specific payment failure information to customers.

{% hint style="danger" %}
Do not display the `failureCode` to end customers. Doing so potentially aids malicious and fraudulent actors.
{% endhint %}

### The fraud block event <a href="#the-fraud-review-failure-event" id="the-fraud-review-failure-event"></a>

![](<../.gitbook/assets/order.blocked event.svg>)

When Digital River detects an anomaly during its [fraud review](orders/the-order-lifecycle.md#fraud-review), or we determine that the customer is on the [Denied Persons List](https://www.bis.doc.gov/index.php/policy-guidance/lists-of-parties-of-concern/denied-persons-list), we create an `order.blocked` event. The payload of this event consists of an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) whose [`state`](orders/the-order-lifecycle.md#order-states-and-events) is `blocked`. The order's [`fraudState`](orders/the-order-lifecycle.md#fraud-review) is also `blocked`. Since these are both terminal states, you should inform end customers that the transaction has failed.

### The pending charge authorization event <a href="#the-pending-payment-event" id="the-pending-payment-event"></a>

![](<../.gitbook/assets/order.pending\_payment event.svg>)

An `order.pending_payment` event indicates that Digital River detected no fraudulent activity during its [fraud review](orders/the-order-lifecycle.md#fraud-review). However, don't use this event as a trigger to initiate fulfillment operations. This is because the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `payment.charges[]` are not yet fully authorized.

For more information, refer to [handling pending payment orders](creating-and-updating-an-order.md#handling-pending-payment-orders).

### The in-process fraud review event <a href="#the-fraud-review-failure-event" id="the-fraud-review-failure-event"></a>

![](<../.gitbook/assets/order.review\_opened event.svg>)

An `order.review_opened` event indicates that Digital River is conducting a secondary fraud review and has moved the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` to [`in_review`](orders/the-order-lifecycle.md#order-states-and-events). Since the fraud review process is not yet complete, don't use this event as a trigger to initiate fulfillment operations.

For more information, refer to [handling in review orders](creating-and-updating-an-order.md#handling-in-review-orders).

### The order accepted event <a href="#listening-for-the-order-accepted-event" id="listening-for-the-order-accepted-event"></a>

![](<../.gitbook/assets/order.accepted event.svg>)

When all of an order's [`payment.charges[]`](orders/payment-charges/#how-a-charge-is-created) are authorized and no irregularities are detected during the [fraud review](orders/the-order-lifecycle.md#fraud-review), Digital River creates an [`order.accepted`](events-and-webhooks-1/events-1/event-types.md#order.accepted) event. Respond to this event by moving the commerce platform's order into a ready to fulfill state.

Unless you [synchronously receive an order in an `accepted` state](creating-and-updating-an-order.md#accepted), your integration should wait until it receives `order.accepted` before initiating [fulfillment operations](fulfillments.md). Doing so reduces the risk of fraud and the frequency of [disputes and chargebacks](returns-and-refunds-1/disputes-and-chargebacks.md).

In the [`data.object`](events-and-webhooks-1/events-1/#event-data) of the [expanded version](events-and-webhooks-1/events-1/#expanded-events) of `order.accepted`, you can use `physical` in each `items[].productDetails` to determine whether that product is classified as physical or digital. If `physical` is `true`, then the product needs to be shipped to the customer. As a result, you should pass its details in an ship request to your fulfillment service. Otherwise, if `false`, then the product is a digital item and should be delivered to the customer via email or some other digital channel.

For more information, refer to [handling accepted orders](creating-and-updating-an-order.md#handling-accepted-orders).

### The order cancelled event

When an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](orders/the-order-lifecycle.md#order-states-and-events) moves to `cancelled`, Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is [`order.cancelled`](events-and-webhooks-1/events-1/event-types.md#order.cancelled) and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) contains that [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

If you decide to build your integration so that customers can submit line-item level cancellation requests (as opposed to the more standard full order cancellations), then you can’t always use `order.cancelled` to trigger [notifications that inform customers their request was successfully processed](customer-notifications.md#successful-cancellation). This is due to the fact that an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` doesn't move to `cancelled` until the [`state`](orders/payment-charges/#the-charge-lifecycle) of all of its [`payment.charges[]`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) is also `cancelled`.

You should also be aware that `order.cancelled` is often created when customers fail to transfer payment by a designated date and time. This applies to [wire transfers](../payments/supported-payment-methods/wire-transfer.md), [Konibini](../payments/supported-payment-methods/konbini.md), and other [`type`](../payments/payment-sources/#supported-payment-methods)(s) of [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that have a [`flow`](../payments/payment-sources/#authentication-flow) of `receiver`.

For example, after an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) with a [primary source](../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) [`type`](../payments/payment-sources/#supported-payment-methods) of `wireTransfer` is created, that order's [`state`](orders/the-order-lifecycle.md#order-states-and-events) typically becomes `pending_payment`. As a result, customers are provided instructions on how to authorize payment. For details, refer to [Handling pending payments](creating-and-updating-an-order.md#handling-pending-payment-orders).&#x20;

If these instructions aren't followed (i.e., the funds aren't pushed within the allotted time), then the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) expires, no [charge authorization](orders/payment-charges/#how-a-charge-is-created) is created, and Digital River creates `order.cancelled`.&#x20;

For more details, refer to [Handling cancelled orders](creating-and-updating-an-order.md#handling-the-order.cancelled-event).

## Handling order state changes <a href="#responding-to-order-states" id="responding-to-order-states"></a>

The following provides information on how to handle [pending payment](creating-and-updating-an-order.md#handling-pending-payment-orders), [in review](creating-and-updating-an-order.md#handling-in-review-orders), [accepted](creating-and-updating-an-order.md#handling-accepted-orders), [cancelled](creating-and-updating-an-order.md#handling-the-order.cancelled-event) orders.

### Handling pending payment orders

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is `pending_payment`, then the [charge](orders/payment-charges/) on the [primary payment `sources[]`](../payments/payment-sources/using-the-source-identifier.md#primary-versus-secondary-sources) is not yet authorized and the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) goods should not be fulfilled.

To handle this `state` change event, determine the value of the order's [`payment.session.nextAction.action`](../integration-options/checkouts/creating-checkouts/payment-sessions.md#next-action).

* If it's `redirect`, refer to [Handling redirect payment methods](../integration-options/checkouts/building-you-workflows/handling-redirect-payment-methods.md).
* If it's `show_payment_instructions`, refer to [Handling delayed payment methods](../integration-options/checkouts/building-you-workflows/handling-delayed-payment-methods.md).

### Handling in review orders

[Orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) that are `in_review` should _not_ be fulfilled. After an order transitions out of this [`state`](orders/the-order-lifecycle.md#order-states-and-events), Digital River creates either [`order.accepted`](creating-and-updating-an-order.md#listening-for-the-order-accepted-event) or [`order.blocked`](creating-and-updating-an-order.md#the-fraud-review-failure-event). So make sure your integration is set up to handle both of these events.

### Handling accepted orders

When an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](orders/the-order-lifecycle.md#order-states-and-events) becomes `accepted`, move the order in your system into a ready to fulfill state.

Depending on whether the order is [synchronously](creating-and-updating-an-order.md#201-created) or [asynchronously](creating-and-updating-an-order.md#listening-for-the-order-accepted-event) accepted, you should also redirect customers to an order confirmation page and/or send them an [order confirmation notification](customer-notifications.md#order-confirmation).

At this point, [fulfillment operations](fulfillments.md) can be initiated.

### Handling the `order.cancelled` event

Upon receiving the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of [`order.cancelled`](creating-and-updating-an-order.md#the-order-cancelled-event), we recommend that you:

* Update the master order record in your system
* Notify customers (typically by email) that their order has been successfully cancelled and no payment was collected. In the email, we suggest you provide:
  * The order number
  * The order cancellation date (you can retrieve this information from the order's `stateTransitions.cancelled` attribute)
  * An itemization of the cancelled goods
  * The payment method used by the customer
  * The total amount cancelled
  * The customer’s billing address
  * Your contact information

## Reusing the checkout identifier

If you attempt to pass a `checkoutId` in a `POST /orders` request, and that Checkout has already been consumed by a different `POST /orders` request, you'll get back a response with a `404 Not Found` status:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "not_found",
            "parameter": "orderId",
            "message": "Order 180139250336 not found"
        }
    ]
}
```
{% endtab %}
{% endtabs %}
