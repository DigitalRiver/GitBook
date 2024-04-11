---
description: Learn how to handle order failures.
---

# Handling a rejected order

On occasion, when you [submit an order](creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the request may be rejected. How you should handle these rejected `POST /orders` depends on whether you receive a [`409` response status code](resubmitting-an-order.md#409-response-status-code) or a [non-`409` response in the `4xx` range](resubmitting-an-order.md#non-409-response-status-code-in-the-4xx-range).

{% hint style="info" %}
If your integration is on version `2021-03-23` or higher, you can use a [checkout's payment session](../integration-options/checkouts/creating-checkouts/payment-sessions.md#how-to-determine-when-to-create-an-order) to determine when a checkout can be successfully converted to an order. By [ensuring the payment session is in the correct state](../integration-options/checkouts/creating-checkouts/payment-sessions.md#session-state), you can greatly minimize order failures.
{% endhint %}

## `409` response status code

If you submit a [`POST /orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders), and receive a `409` response status code, you can use the `type`, `code`, and `message` contained in the error to help diagnose the failure. Once you isolate the problem, however, you can't simply update the checkout. Instead, you must create a _new_ checkout and send its identifier in the payload of a create order request.

Order failures with a `409` response status code are often due to [charge authorization declines](../payments/authorization-declines.md) that result from insufficient funds or lack of credit. If this is the case, you should obtain new payment method information from the customer, use it to [create a source](../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) and then [attach the source to the new checkout](../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts). Alternatively, in the case of [registered checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices), you could [authenticate one of the customer's existing payment sources](../payments/payment-sources/using-the-source-identifier.md#authenticating-sources) and then attach the source to the checkout.

## non-`409` response status code in the `4xx` range

If you submit a [`POST /orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createOrders), and receive a non-`409` response status code in the `4xx` range , you can use the `type`, `code`, and `message` contained in the error to help diagnose the failure. Once you isolate the problem, you can modify the existing checkout, send a `POST /checkouts/{id}`, and then attempt to resubmit the order. In other words, in this scenario, you can send the same checkout identifier in the payload of a create order request.

{% hint style="warning" %}
You cannot however [re-use a checkout identifier](creating-and-updating-an-order.md#reusing-the-checkout-identifier) once it's been sent in the payload of a successful `POST  /orders` request.
{% endhint %}
