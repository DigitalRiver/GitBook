---
description: >-
  Learn how to inform Digital River that products are fulfilled or cancelled so
  that we can attempt to capture or cancel payment
---

# Capturing and cancelling charges

Once you [create an order](creating-and-updating-an-order.md), and [handle the necessary events](informing-digital-river-of-a-fulfillment.md#receiving-the-necessary-events), you can use the [Fulfillments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) to notify Digital River of fulfilled and/or cancelled items. Each time you [define](informing-digital-river-of-a-fulfillment.md#defining-fulfillments) and [submit](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests) a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) request, you're informing our payment services how many items in an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) are fulfilled and/or cancelled. We then use that information to [capture](orders/payment-charges/#captures) or [cancel](orders/payment-charges/#cancels) the appropriate amount of an order's payment [charges](orders/payment-charges/).

Once you submit a `POST/fulfillments`, your integration should also be set up to [handle fulfillment-related events](informing-digital-river-of-a-fulfillment.md#using-fulfillment-related-events).

## Receiving the necessary events <a href="#receiving-the-necessary-events" id="receiving-the-necessary-events"></a>

Before you submit a [`POST/fulfillment`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) request, you must first receive and handle the necessary events. The specific events you must process depend on the order's [fulfillment model](fulfillments.md):

|                                                                                           Upstream requirement                                                                                           | Digital River coordinated fulfillments (distributed model) | Digital River coordinated fulfillments (orchestrated model) | Third party coordinated fulfillments |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------: | :---------------------------------------------------------: | :----------------------------------: |
|                   An [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](orders/the-order-lifecycle.md#order-states-and-events) state                  |                              ✔                             |                                                             |                   ✔                  |
|   The [`fulfillment_order.shipped`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#listening-and-responding-to-fulfillment-order-events) event  |                              ✔                             |                                                             |                                      |
| The [`fulfillment_order.cancelled`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#listening-and-responding-to-fulfillment-order-events) event​ |                              ✔                             |                                                             |                                      |

### Third party coordinated fulfillments

In [third-party coordinated fulfillments](fulfillments.md#third-party-coordinated-fulfillments), you need to [synchronously](creating-and-updating-an-order.md#accepted) or [asynchronously](creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](orders/the-order-lifecycle.md#order-states-and-events) state.

In most integrations, you respond to this order state change by sending a fulfillment request to your logistics partner and when the products are shipped, your partner sends you a shipment notification. You should respond to this notification by [defining a `POST/fulfillments`](informing-digital-river-of-a-fulfillment.md#defining-fulfillments) with the `quantity` of each shipped line item and then [submitting the payment capture request](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

Similarly, when an item is successfully cancelled, your fulfiller typically sends you a cancelled shipment notification. Respond to this notification by [defining a `POST/fulfillments`](informing-digital-river-of-a-fulfillment.md#defining-fulfillments) with the `cancelQuantity` of each cancelled line item and then [submitting the payment cancel request](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

### Digital River coordinated fulfillments

In [Digital River coordinated fulfillments](fulfillments.md#digital-river-coordinated-fulfillments), the specific events you must process depends on whether you're using the distributed model or the orchestrated model.

#### Distributed model

In the [distributed model](fulfillments.md#assisted-fulfillment-model), you need to handle an [`accepted`](orders/the-order-lifecycle.md#order-states-and-events) order by [creating a fulfillment order](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#creating-a-fulfillment-order). You must then wait to receive a [`fulfillment_order.shipped`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#shipped-events) event before handling that by [defining a `POST/fulfillments`](informing-digital-river-of-a-fulfillment.md#defining-fulfillments) with the `quantity` of each shipped line item and then [submitting the payment capture request](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

Similarly, in this model, you must also wait to receive a [`fulfillment_order.cancelled`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#cancelled-events) event before handling that by [defining a `POST/fulfillments`](informing-digital-river-of-a-fulfillment.md#defining-fulfillments) with the `cancelQuantity` of each cancelled line item and then [submitting the payment cancel request](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

#### Orchestrated model

In the [orchestrated model](fulfillments.md#automated-fulfillment-model)**,** you don't need to respond to any of these events. Our orchestration service monitors the key commerce and fulfillment events and then handles the payment [capture](orders/payment-charges/#captures) and [cancel](orders/payment-charges/#cancels) process.

## Defining fulfillments

Once you [receive and handle the necessary events](informing-digital-river-of-a-fulfillment.md#receiving-the-necessary-events), define a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) request.

You do this by providing an [order identifier](orders/#unique-identifier), information about [each fulfilled and/or cancelled item](informing-digital-river-of-a-fulfillment.md#fulfilled-and-cancelled-items), as well as any [shipment identifiers](informing-digital-river-of-a-fulfillment.md#shipment-identifiers) and [tracking data](informing-digital-river-of-a-fulfillment.md#shipment-identifiers) provided by your fulfiller.

### Fulfilled and cancelled items

In the request's `items` array, you specify each [line item's](orders/#line-items) unique identifier and the quantity fulfilled and/or cancelled. The request doesn't need to specify both a `quantity` and `cancelQuantity`, but it must contain one or the other.

If you specify a `quantity`, thereby informing our payment services that these items are fulfilled, we attempt to [capture](orders/payment-charges/#captures) the appropriate amount of the [payment charge](orders/payment-charges/). Conversely, if you specify a `cancelQuantity`, we attempt to [cancel](orders/payment-charges/#cancels) the relevant charge amount.

### Shipment identifiers

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/) that use the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model), a `POST /fulfillments` must include a single `shipmentId` and one or more  `items[].shipmentItemId`(s).

To obtain these identifiers, [configure a webhook](events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a `type` of [`fulfillment_order.shipped`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#shipped-events) event and then pass them in the body of a  `POST /fulfillments`.

### Tracking data

You can also include information on the name of the `trackingCompany`, the `trackingNumber` provided by the shipping carrier, and the `trackingUrl` that customers use to monitor the shipment.

In [third-party coordinated fulfillments](fulfillments.md#third-party-coordinated-fulfillments), you typically receive this tracking information from your fulfiller when they notify you of a shipment.

In [Digital River coordinated fulfillments](fulfillments.md#digital-river-coordinated-fulfillments) that use the[ distributed model](fulfillments.md#assisted-fulfillment-model), you can retrieve this information from the [`fulfillment_order.shipped`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#shipped-events) event.

## Submitting payment capture and cancellation requests <a href="#submitting-fulfillment-and-cancellation-requests" id="submitting-fulfillment-and-cancellation-requests"></a>

Each time you send a `POST/fulfillments` and receive a `201 Created`, the payload contains a [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) with a unique identifier. The request also triggers a [`fulfillment.created`](informing-digital-river-of-a-fulfillment.md#handling-the-fulfillment-created-event) event.

{% tabs %}
{% tab title="POST/fulfillments" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/fulfillments' \
...
--data-raw '{
  "orderId": "231388420336",
  "items":
    [
      {
        "itemId": "158140150336",
        "quantity": "2"
      }
    ]
}'
```
{% endtab %}

{% tab title="Fulfillment" %}
```javascript
{
    "id": "ful_14776912-d0ff-4f11-974f-17b0f2830ea2",
    "createdTime": "2022-07-01T17:55:58Z",
    "items": [
        {
            "quantity": 2,
            "cancelQuantity": 0,
            "skuId": "b0fd7334-8f7d-424e-b535-308fae972461",
            "itemId": "158140150336"
        }
    ],
    "orderId": "231388420336",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

## Handling fulfillment-related events <a href="#using-fulfillment-related-events" id="using-fulfillment-related-events"></a>

Depending on your integration, you might find it useful to subscribe to the [fulfillment created event](informing-digital-river-of-a-fulfillment.md#handling-the-fulfillment-created-event). We recommend however that all integrations handle [charge capture](informing-digital-river-of-a-fulfillment.md#handling-charge-capture-complete-and-failed-events), [charge cancel](informing-digital-river-of-a-fulfillment.md#the-charge-cancel-success-event), [order fulfilled](informing-digital-river-of-a-fulfillment.md#the-order-fulfilled-event), and [order complete](informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event) events.

### Fulfillment created event <a href="#handling-the-fulfillment-created-event" id="handling-the-fulfillment-created-event"></a>

The `data.object` of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of [`fulfillment.created`](events-and-webhooks-1/events-1/event-types.md#fulfillment.created) contains a [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) and `orderDetails`. The event's `orderDetails` has nearly all the same data as the associated [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). The primary exception is that `orderDetails` doesn't contain the order's `payment`.&#x20;

{% hint style="info" %}
You can also access `orderDetails` by [retrieving the fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillments).&#x20;
{% endhint %}

Having `orderDetails` in `fulfillment.created` allows you to directly access the data needed to define [shipment confirmation](customer-notifications.md#shipment-notification) and/or [cancellation confirmation](customer-notifications.md#successful-cancellation) email notifications without having to retrieve `orderId` and make a [get order request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveOrders).&#x20;

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/) that use the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), the `fulfillment.created` event can also be useful for accessing tracking data. The event provides a `trackingCompany` name, a `trackingNumber`, and a `trackingUrl`.

{% hint style="info" %}
You can also obtain this data from the [`fulfillment_order.shipped`](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#shipped-events) event.
{% endhint %}

```javascript
{
    "id": "5203007c-c3e9-47f0-a5aa-51e512fbd3ea",
    "type": "fulfillment.created",
    "data": {
        "object": {
            "id": "ful_c34fd193-94a6-469f-89c2-fd09f50827be",
            ...
            "shipmentId": "100002369153",
            "trackingCompany": "Fedex",
            "trackingNumber": "Z10100002632653",
            "trackingUrl": "http://www.fedex.com/Tracking?tracknumbers=Z10100002632653",
            ...
        }
    },
    ...
}
```

In this case, you could use the event to trigger a shipped notification to the customer (typically an email) that contains this tracking information and/or add it to the customer's order management page.

### Charge capture complete and failed events <a href="#handling-charge-capture-complete-and-failed-events" id="handling-charge-capture-complete-and-failed-events"></a>

Your integration should be set up to handle [`order.charge.capture.complete`](informing-digital-river-of-a-fulfillment.md#successful-charge-captures) and [`order.charge.capture.failed`](informing-digital-river-of-a-fulfillment.md#failed-charge-captures) events. The payload of both consists of a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) and contains a `fulfillmentId` that identifies the [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) which triggered the event.

#### Successful charge captures

An `order.charge.capture.complete` event indicates that Digital River fully or partially captured one of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [charges](orders/payment-charges/).

{% hint style="info" %}
In the following example, the charge's [`state`](orders/payment-charges/#the-charge-lifecycle) remains `capturable` because the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is only partially fulfilled.
{% endhint %}

{% tabs %}
{% tab title="order.charge.capture.complete" %}
```javascript
{
    "id": "f275be0a-45fd-4160-8a31-b3274b6a4f8b",
    "type": "order.charge.capture.complete",
    "data": {
        "object": {
            "id": "b67136cc-0b2e-43f7-8d9a-362047aa975a",
            "createdTime": "2022-03-02T16:50:23Z",
            "currency": "USD",
            "amount": 37.81,
            "state": "capturable",
            "orderId": "218377480336",
            "captured": true,
            "captures": [
                {
                    "id": "b496b7b2-3bc7-49cd-ab48-f91b2f2e37cc",
                    "createdTime": "2022-03-02T16:50:37Z",
                    "amount": 25.21,
                    "state": "complete",
                    "fulfillmentId": "ful_a0246997-bdcf-480a-a066-2cfc564e6232"
                }
            ],
            "refunded": false,
            "sourceId": "52ca4456-5547-4f9c-8016-1a067fd0b125",
            "paymentSessionId": "7c121712-2ae8-4617-97a2-5d41fd79a5b8",
            "type": "customer_initiated",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-02T16:52:01.180061Z",
    ...
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

You can handle this event by notifying customers of the amount captured, the payment method used to make the capture, relevant product details, and any shipment tracking information that may be available.

The event's `captures[].amount` and `captures[].createdTime` provides the data you need to inform customers how much and when they were charged.

To access data on the [payment source](../payments/payment-sources/) associated with the capture, pass the event's `sourceId` as a path parameter in a [`GET/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources).

In this example, the customer used a credit card, so from the `200 OK` response you'd most likely retrieve `creditCard.brand` and `creditCard.lastFourDigits`.

{% tabs %}
{% tab title="Source" %}
```javascript
{
    "id": "52ca4456-5547-4f9c-8016-1a067fd0b125",
    "createdTime": "2022-03-02T16:49:48Z",
    "type": "creditCard",
    "reusable": false,
    "state": "consumed",
    ...
    "clientSecret": "52ca4456-5547-4f9c-8016-1a067fd0b125_ae8fb67f-bcf4-49ac-9a6d-3427ce5d5f20",
    "creditCard": {
        "brand": "Visa",
        "expirationMonth": 7,
        "expirationYear": 2027,
        "lastFourDigits": "1111"
    },
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

To access product and tracking data, use the event's `captures[].fulfillmentId` to [retrieve the fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillments) that triggered the capture.&#x20;

From the `200 OK` response, you can use `orderDetails.items[].productDetails` to get each product's `name`, `description`, `image`, and other data. Depending on your integration, the [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) may also contain [shipment tracking data](informing-digital-river-of-a-fulfillment.md#tracking-data).

{% tabs %}
{% tab title="Fulfillment" %}
{% code title="200 OK" %}
```javascript
{
    "id": "ful_e2713c40-1c9e-4c47-a047-7344a4ea34c4",
    "createdTime": "2022-07-01T18:30:59Z",
    "items": [
        {
            "quantity": 2,
            "cancelQuantity": 0,
            "skuId": "eecf60da-b082-47eb-9a3f-602820f22ed9",
            "itemId": "158140510336"
        }
    ],
    "orderId": "231388760336",
    "liveMode": false,
    "chargeOperationIds": [
        "9f1367e8-531c-4ca9-ac2d-8b940cf074f9"
    ],
    "orderDetails": {
        "id": "231388760336",
        "createdTime": "2022-07-01T18:30:44Z",
        "currency": "USD",
        "email": "chaseMarshall@digitalriver.com",
        "shipTo": {
            "address": {
                "line1": "1234 Any Road W",
                "city": "Minneapolis",
                "postalCode": "55401",
                "state": "MN",
                "country": "US"
            },
            "name": "Chase Marshall"
        },
        "shipFrom": {
            "address": {
                "country": "US"
            }
        },
        "billTo": {
            "address": {
                "line1": "Any other road W",
                "city": "Eagan",
                "postalCode": "55122",
                "state": "MN",
                "country": "US"
            },
            "name": "Chase Marshall",
            "email": "marshallsBillingEmail@digitalriver.com"
        },
        "totalAmount": 27.01,
        "subtotal": 25.0,
        "totalFees": 0.0,
        "totalTax": 2.01,
        "totalImporterTax": 0.0,
        "totalDuty": 0.0,
        "totalDiscount": 0.0,
        "totalShipping": 5.0,
        "items": [
            {
                "id": "158140510336",
                "skuId": "eecf60da-b082-47eb-9a3f-602820f22ed9",
                "productDetails": {
                    "id": "eecf60da-b082-47eb-9a3f-602820f22ed9",
                    "name": "Widget",
                    "description": "A small gadget or mechanical device",
                    "countryOfOrigin": "US",
                    "weight": 10,
                    "weightUnit": "g",
                    "partNumber": "eecf60da-b082-47eb-9a3f-602820f22ed9"
                },
                "amount": 20.0,
                "quantity": 2,
                "state": "fulfilled",
                "stateTransitions": {
                    "created": "2022-07-01T18:30:44Z",
                    "fulfilled": "2022-07-01T18:31:00Z"
                },
                "tax": {
                    "rate": 0.08025,
                    "amount": 1.61
                },
                "importerTax": {
                    "amount": 0.0
                },
                "duties": {
                    "amount": 0.0
                },
                "availableToRefundAmount": 27.01,
                "fees": {
                    "amount": 0.0,
                    "taxAmount": 0.0
                }
            }
        ],
        "shippingChoice": {
            "id": "123",
            "amount": 5.0,
            "description": "standard",
            "serviceLevel": "SG",
            "taxAmount": 0.4,
            "shippingTerms": "DDP"
        },
        "updatedTime": "2022-07-01T18:31:37Z",
        "locale": "en_US",
        "customerType": "individual",
        "sellingEntity": {
            "id": "C5_INC-ENTITY",
            "name": "DR globalTech Inc."
        },
        "liveMode": false,
        "state": "complete",
        "stateTransitions": {
            "fulfilled": "2022-07-01T18:31:00Z",
            "accepted": "2022-07-01T18:30:47Z",
            "complete": "2022-07-01T18:31:37Z"
        },
        "fraudStateTransitions": {
            "passed": "2022-07-01T18:30:47Z"
        },
        "requestToBeForgotten": false,
        "capturedAmount": 27.01,
        "cancelledAmount": 0.0,
        "availableToRefundAmount": 27.01,
        "checkoutId": "0f4d5515-c56c-450c-ad71-073e00276df4"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

You can use the the event's `orderId` to look up the order in your system and provide some or all of this capture, payment, product, and shipping information on the customer's order details page. For example:

_We billed your `creditCard.brand` ending in `creditCard.lastFourDigits` in the amount of `captures[].amount` on `captures[].createdTime`_. _This payment is for the following products:_

* _`name` | `description` | `image`_

#### Failed charge captures

In rare cases, a [capture](orders/payment-charges/#the-charge-lifecycle) fails. If this happens, Digital River creates an `order.charge.capture.failed` event.

To handle this event, we recommend that you:

* Send a shipment cancellation request to your fulfillment logistics partner. The event's `captures[].fulfillmentId` allows you to [retrieve the fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveFulfillments), access its `shipmentId` and `items[].shipmentItemId` and then use these identifiers to cancel the shipment.\
  \
  Make sure you check with your fulfiller to determine whether they have the ability to cancel a shipment within a certain window of time. If you're using [Digital River's fulfillment service](fulfillments.md#digital-river-coordinated-fulfillments), refer to [Cancelling physical fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/instructing-digital-to-cancel-items.md).&#x20;
* Contact the customer to arrange a return or alternate payment.

Failed captures are usually due to expired charge authorizations. This might happen when you're running a pre-order sale and there's a lengthy period between submission of a [`POST/orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders) that [authorizes the charge](orders/payment-charges/#how-a-charge-is-created) and a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) that [captures](orders/payment-charges/#captures) payment.

Failed captures might also be due to fulfillment delays on the part of your logistics partner.

{% hint style="success" %}
On the [Testing scenarios](../developer-resources/testing-scenarios.md) page, we provide [credit card information](../developer-resources/testing-scenarios.md#error-scenarios-2) that you can use to check how your integration handles failed charge captures.
{% endhint %}

{% tabs %}
{% tab title="order.charge.capture.failed" %}
```javascript
{
    "id": "61b66e77-cc9a-4144-b048-f0bf06aff777",
    "type": "order.charge.capture.failed",
    "data": {
        "object": {
            "id": "3b4ef391-e8ae-412a-994b-df3e447aafa0",
            "createdTime": "2022-03-02T17:38:35Z",
            "currency": "USD",
            "amount": 37.81,
            "state": "capturable",
            "orderId": "218378950336",
            "captured": true,
            "captures": [
                {
                    "id": "7542f424-7615-4748-8af6-9c04001ce2e8",
                    "createdTime": "2022-03-02T17:38:51Z",
                    "amount": 37.81,
                    "state": "failed",
                    "failureCode": "failed-request",
                    "fulfillmentId": "ful_2bbb92e0-16fa-4a62-952e-4e2ca4df2870"
                }
            ],
            "refunded": false,
            "sourceId": "e13b2327-d94d-4a62-821c-f11693e64ede",
            "paymentSessionId": "d149962c-80fc-4f7b-b4fc-bc8a80482aef",
            "type": "customer_initiated",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-02T17:38:54.966905Z",
    ...
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

The failed capture event contains a `failureCode`. We also provide a `failureMessage` that may help diagnose the issue. To access this message:

1. Save the unique `id` of the event's capture.
2. Retrieve the event's `data.object.id`, which uniquely identifies the [charge](orders/payment-charges/).
3. Send this charge identifier as a path parameter in a [`GET/charges/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCharges).
4. In the `200 OK` response, use the saved capture identifier to search `captures[]` for the appropriate element and retrieve its `failureMessage`.

In nearly all cases, however, `failureCode` is `failed-request` and `failureMessage` is `Failed to operate on charge`. This indicates that Digital River was unable to determine a reason for the capture failure.

### The charge cancel success event <a href="#the-charge-cancel-success-event" id="the-charge-cancel-success-event"></a>

We recommend that your integration be setup to handle successful [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) cancellations.

The `order.charge.cancel.complete` event typically originates with a customer making a request on your site to cancel an entire [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) (or a certain quantity of one or more [line items](creating-and-updating-an-order.md#line-items) in an order).

This request, in turn, should eventually trigger a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) that specifies a `cancelQuantity` for each line item that the customer wants to cancel.

{% hint style="info" %}
In [physical fulfillments](../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), make sure you send a shipment cancellation request to your fulfiller, and receive a successful response, before sending the [charge cancellation request to Digital River](informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

For [Digital River coordinated fulfillments](fulfillments.md#digital-river-coordinated-fulfillments), refer to [Cancelling physical fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/instructing-digital-to-cancel-items.md).
{% endhint %}

{% tabs %}
{% tab title="order.charge.cancel.complete" %}
```javascript
{
    "id": "96640a35-40bc-4e44-8b33-34c623fd3713",
    "type": "order.charge.cancel.complete",
    "data": {
        "object": {
            "id": "66ebb961-c60e-49d8-9dce-32f6be1e770e",
            "createdTime": "2021-10-05T09:07:06Z",
            "currency": "USD",
            "amount": 54.1,
            "state": "capturable",
            "orderId": "201293880336",
            "captured": false,
            "refunded": false,
            "cancels": [
                {
                    "id": "9c755ce0-b52d-4a77-97d7-c7ed73931156",
                    "createdTime": "2021-10-05T09:07:15Z",
                    "amount": 10.82,
                    "state": "complete"
                }
            ],
            "sourceId": "a7e5633f-572c-4a7b-9991-e8ff2f3a2f7a",
            "paymentSessionId": "beaaa4cb-67fd-43fa-b57d-7b0b447afc60",
            "type": "customer_initiated",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2021-10-05T09:07:17.160189Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "8044a862-e7c9-4a8f-a3bb-b6b987a2be9e"
    ],
    "digitalriverVersion": "2021-03-23"
}
```
{% endtab %}
{% endtabs %}

Upon receipt of the charge cancellation event, inform customers of the cancelled payment.

To do this, retrieve the event's `orderId`, `cancels[].createdTime` and `cancels[].amount`. To access information about the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), retrieve the event's `sourceId` and pass it as a path parameter in a [`GET/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources).

In this example order, the customer used a credit card, so you'd retrieve `creditCard.brand` and `creditCard.lastFourDigits` from the response.

{% tabs %}
{% tab title="Source" %}
```javascript
{
    "id": "a7e5633f-572c-4a7b-9991-e8ff2f3a2f7a",
    "createdTime": "2021-10-05T09:06:58Z",
    "type": "creditCard",
    "reusable": false,
    "state": "consumed",
    "owner": {
        "firstName": "Guy",
        "lastName": "Incognito",
        "email": "guy@example.org",
        "address": {
            "line1": "1234 St.",
            "city": "Minnetonka",
            "postalCode": "55341",
            "state": "MN",
            "country": "US"
        }
    },
    "clientSecret": "a7e5633f-572c-4a7b-9991-e8ff2f3a2f7a_caa2ec51-453b-4f29-971d-cb6ffc594e22",
    "creditCard": {
        "brand": "Visa",
        "expirationMonth": 10,
        "expirationYear": 2022,
        "lastFourDigits": "1111"
    },
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

You can use the event's `orderId` to locate the order in your system and display the cancel payment information to customers on their order details page. For example:

_On_ _`cancels[].createdTime` we cancelled billing on your `creditCard.brand` ending in `creditCard.lastFourDigits` in the amount of `cancels[].amount`._

### The order fulfilled event

Once you submit one or more `POST/fulfillments` that result in every [line item's](creating-and-updating-an-order.md#line-items) `state` transitioning to `fulfilled`, then the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` also becomes `fulfilled` and an `order.fulfilled` event is fired.

{% hint style="info" %}
If you use a third-party service to generate customer notifications, refer to [How Digital River returns product data](../integration-options/checkouts/creating-checkouts/describing-the-items/#how-digital-river-returns-product-data) for details on how that service can use this event.
{% endhint %}

At this point, if you submit any additional `POST/fulfillments` on the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), you receive the following error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "order_fulfilled",
            "parameter": "orderId",
            "message": "Resource '201454110336' is fulfilled."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

If your integration is set up to respond to shipment notifications from your fulfiller by synchronously submitting a `POST/fulfillments`, then you can use `order.fulfilled` as a trigger to send a notification to customers informing them that all of an order's goods have been shipped.

### The order complete event <a href="#handling-the-order-complete-event" id="handling-the-order-complete-event"></a>

When the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) moves into a [`complete`](orders/the-order-lifecycle.md#order-states-and-events) state, an `order.complete` event is fired. Upon receipt of this event, use the event's `data.object.id` or `data.object.upstreamId` to look up the order in your system and set its status to complete.

{% hint style="info" %}
If you use a third-party service to generate customer notifications, refer to [How Digital River returns product data](../integration-options/checkouts/creating-checkouts/describing-the-items/#how-digital-river-returns-product-data) for details on how that service can use this event.
{% endhint %}

The `order.complete` event can also act as a trigger to populate the customer's order details page. The following lists some of the information you may decide to display on this page, along with the field in the event that contains the data. Most likely, you've already used prior API responses and events to store much of this data in your system.

| Order details page             | Event's data.object field                  |
| ------------------------------ | ------------------------------------------ |
| Order number                   | `id`                                       |
| Date of order                  | `createdTime`                              |
| Shipping address               | `shipTo.address`                           |
| Billing address                | `billTo.address`                           |
| Order total                    | `totalAmount`                              |
| Total before tax               | `subtotal`                                 |
| Fees                           | `totalFees`                                |
| Taxes                          | `totalTax`                                 |
| Duties                         | `totalDuty`                                |
| Shipping and handling          | `totalShipping`                            |
| Product details                | `items[].productDetails`                   |
| Product cost                   | `items[].amount`                           |
| Product quantity               | `items[].quantity`                         |
| Payment method(s)              | `payment.sources[].type`                   |
| Billing date(s)                | `payment.charges[].captures[].createdTime` |
| Billing amount(s)              | `payment.charges[].captures[].amount`      |
| Billing cancellation date(s)   | `payment.charges[].cancels[].createdTime`  |
| Billing cancellation amount(s) | `payment.charges[].cancels[].amount`       |

You can also use `order.complete` as a trigger to activate a request refund button on the customer's order details page. When handling the button's click event, make sure you use the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) to [process the request](returns-and-refunds-1/refunds/issuing-refunds.md).
