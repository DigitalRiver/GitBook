---
description: Learn how a standard flow works in the Direct Integrations option
---

# Standard flow

The following sequence diagrams outline a standard [Direct Integrations](./) flow. They depict interactions between the customer, your commerce platform, the Digital River APIs, and Digital River. These diagrams are meant to outline Digital River's core capabilities, focusing specifically on:

* Important states in an [order's life cycle](../../order-management/orders/the-order-lifecycle.md)
* The sequence of major [events](../../order-management/events-and-webhooks-1/events-1/)
* The data you must provide to utilize Digital River's [authorized reseller of record](../../) business model
* How checkouts, orders, events, and fulfillments work

To learn about other flows, refer to the [Sequence diagrams](../../general-resources/standards-and-certifications/integration-checklists/#sequence-diagram) section on the [Integration checklists](../../general-resources/standards-and-certifications/integration-checklists/) page.

## Product management

When identifying and describing your products in the Digital River APIs, you can use several approaches.

For details on your product management options, refer to the [Product basics](../../product-management/skus.md) page.

## Pre-checkout

Digital River is typically not involved in initial pre-checkout interactions between customers and your commerce platform. During this stage, customers land on your storefront, build a cart, confirm the cart's details, and initiate checkout. Your commerce platform typically presents them with the option of checking out as either a [guest or registered customer](creating-checkouts/using-the-checkout-identifier.md).

![](<../../.gitbook/assets/Part 1 (1).png.png>)

## Building a checkout <a href="#creating-a-checkout" id="creating-a-checkout"></a>

When a new customer checks out on your storefront, you can use the Digital River APIs to create a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). The [checkout](creating-checkouts/) contains the transaction's tax details and assigned [selling entity](creating-checkouts/selling-entities.md). Your commerce platform should update the user interface with this tax information and use the selling entity to [display compliance disclosures](../../developer-resources/reference/elements/compliance-elements.md).

![](<../../.gitbook/assets/Part 2.png>)

## Creating an order <a href="#creating-a-source-and-order" id="creating-a-source-and-order"></a>

When customers proceed to the payment entry stage, your commerce platform needs to render [Drop-in payments](../../payments/payment-integrations-1/drop-in/). Customers then submit their payment details and [Drop-in payments](../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md) uses that information to create a payment [source](../../payments/payment-sources/).

{% hint style="success" %}
Explore the [Drop-in payments builder](https://drapi.io/drop-in-builder/) to gain a better understanding of how sources are created.
{% endhint %}

If customers opted to save the payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) for future purchases, and that source is [ready for storage](../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details), you should [attach the source to the customer](../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers) and then [apply the source to the checkout](../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts). Otherwise, simply apply the source to the checkout for use in this [single transaction](../../payments/payment-sources/#reusable-or-single-use).

Once payment is applied, use the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) to update the commerce platform with the transaction's final tax information and [selling entity](creating-checkouts/selling-entities.md). The commerce platform should then render an order review page with the appropriate [compliance information](../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale).

![](<../../.gitbook/assets/Part 3 (2) (1).png>)

At this point, customers typically confirm the transaction's details and submit the order. This event should trigger a [create order request](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). This request primarily acts as a [fraud review](../../order-management/orders/the-order-lifecycle.md#fraud-review) and [payment authorization](../../order-management/orders/payment-charges/#how-a-charge-is-created) call.

The [immediate response](../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response) contains either a `409 Conflict` or `201 Created` status code. In the event of an error, update the status of the commerce platform and render the appropriate message to storefront customers. If an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is created, use the response's data to update the status of the commerce platform's order.

For [immediately accepted orders](../../order-management/creating-and-updating-an-order.md#accepted), move the commerce platform's order into a ready to fulfill state and direct customers to some sort of "Thank You" page.

![](<../../.gitbook/assets/Part 4 (1).png>)

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../order-management/orders/the-order-lifecycle.md) is immediately returned as [pending payment authorization](../../order-management/creating-and-updating-an-order.md#pending-payment) or [in fraud review](../../order-management/creating-and-updating-an-order.md#in-review), you'll need to handle [asynchronous, order-related events](../../order-management/creating-and-updating-an-order.md#listening-for-and-handling-order-related-webhook-events) sent by Digital River.

Once an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is successfully screened for fraud or customers complete the steps necessary to [push payment](../../payments/payment-sources/#pull-or-push), Digital River creates the [order accepted and ready to fulfill event](../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event). If an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) asynchronously fails due to suspected fraud or because the payment window closes without funds, we create an [order blocked](../../order-management/creating-and-updating-an-order.md#the-fraud-review-failure-event) or [charged failed](../../order-management/creating-and-updating-an-order.md#the-payment-failure-event) event, respectively.

When you're notified of one of these [events](../../order-management/events-and-webhooks-1/events-1/), retrieve the order's [`state`](../../order-management/orders/the-order-lifecycle.md) from the event's payload, and, depending on that value, move the commerce platform's order into an accepted, blocked, or payment failed state.

![](<../../.gitbook/assets/Part 5.png>)

## Fulfilling an order

Once an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is [`accepted`](../../order-management/creating-and-updating-an-order.md#handling-accepted-orders), the client can initiate fulfillment. As products are fulfilled or cancelled, the commerce platform updates the status of those line items and emits status change events. These events should trigger a [`POST/fulfillments`](../../order-management/informing-digital-river-of-a-fulfillment.md) request that specifies the fulfilled quantity, the cancelled quantity, or both. Depending on the configuration of that request, Digital River initiates a [funds capture](../../order-management/orders/payment-charges/#captures) and/or [authorization reversal](../../order-management/orders/payment-charges/#cancels).

![](<../../.gitbook/assets/Part 6 (3).png (1).png>)
