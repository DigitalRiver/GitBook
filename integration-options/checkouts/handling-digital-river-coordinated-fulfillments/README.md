---
description: Understand Digital River's fulfillment solutions
---

# Digital River coordinated fulfillments

This section provides an overview of two Digital River coordinated fulfillment models.

Both models allow you to [build checkouts](../creating-checkouts/) with [physical and digital](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) products, [check inventory levels](checking-inventory-levels.md), [process shipping quotes](using-shipping-quotes.md), [reserve inventory](reserving-inventory-items.md), use our [supported payment methods](../../../payments/supported-payment-methods/), [combine payment sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources), [initiate fulfillments](global-fulfillments.md#creating-a-fulfillment-order), [track shipments](global-fulfillments.md#tracking-a-shipment), [cancel fulfillments](instructing-digital-to-cancel-items.md), [capture and cancel payments](../../../order-management/informing-digital-river-of-a-fulfillment.md), and [handle reversals](../../../order-management/returns-and-refunds-1/returns/digital-river-coordinated-returns.md).

In both models, you also use [SKU-inventory item pairs](../../../product-management/common-attributes.md).

The major differences between the [distributed model](./#distributed-model) and the [orchestrated model](./#orchestrated-model) revolve around (1) how you build and maintain your catalog of products whose fulfillment Digital River coordinates and (2) who is responsible for handling order accepted, product shipment, and product cancellation events.

### Distributed model

In the distributed model, as with all Digital River coordinated fulfillments, your [SKU-inventory item pairs](../../../product-management/common-attributes.md) represent products whose fulfillment Digital River coordinates. You create these pairs and are responsible for keeping their data synchronized.

After [converting the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you wait for the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) to be [`accepted`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events) and then handle this `state` change event by [creating a fulfillment order](global-fulfillments.md#creating-a-fulfillment-order). You then listen for [product shipment](global-fulfillments.md#listening-and-responding-to-fulfillment-order-events) and [product cancellations](global-fulfillments.md#monitoring-and-responding-to-a-fulfillment-order) events, and handle them by sending [payment capture and cancellation requests](../../../order-management/informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests).

The following provides a high-level overview of how you might structure a distributed model workflow:

#### Creating and maintaining your product catalog

Prior to deployment, you should build a catalog of [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) whose fulfillment Digital River coordinates. For each product in this catalog, use the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) and [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) to create [SKU-inventory item pairs](../../../product-management/common-attributes.md) with [shared attributes](../../../product-management/common-attributes.md#shared-attributes) and then ensure those attribute values remain synchronized.

It's important that you keep these pairs synchronized. In every [create checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) you must reference the [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) when [describing line items](../creating-checkouts/describing-the-items/). Later, after you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), and the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is [`accepted`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events), you need to reference the paired [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) in a [create fulfillment order request](global-fulfillments.md#creating-a-fulfillment-order).

If the [shared attribute values](../../../product-management/common-attributes.md#shared-attributes) of these SKU-inventory item pairs are not synchronized, you risk encountering problems with customs, generating incorrect duty amounts or having errors displayed on invoices.

{% hint style="info" %}
When [building checkouts](../creating-checkouts/) using the distributed model, you can add [physical SKUs](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) from the catalog of products whose fulfillment Digital River coordinates as well as [digital SKUs](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) from other catalogs.
{% endhint %}

#### Building checkouts and submitting orders

In both this model and the [orchestrated model](./#orchestrated-model), you can use the same basic approach to [process your checkouts and submit your orders](./#structuring-checkout-processing-and-order-submissions).

#### Initiating physical product fulfillment

In the distributed model, once you build the checkout and submit the order, and then either [synchronously](../../../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted` state](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders), you retrieve data from that order and use it to [create a fulfillment order](global-fulfillments.md#creating-a-fulfillment-order).[ ](global-fulfillments.md#creating-a-fulfillment-order)This request instructs Digital River's fulfillment services to initiate fulfillment of the order's physical products.

{% hint style="info" %}
For more information, refer to [handling accepted orders](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders) on the [Processing orders](../../../order-management/creating-and-updating-an-order.md) page.
{% endhint %}

#### Responding to product pending and backordered events

If you give customers the option to cancel orders, then the [`fulfillment_order.pending`](global-fulfillments.md#pending-events) event contains the [fulfillment order identifier and fulfillment order line item identifiers](global-fulfillments.md#unique-identifiers) that you need to [create a fulfillment order cancellation](instructing-digital-to-cancel-items.md#requesting-a-fulfillment-cancellation).

You can also subscribe to the [`fulfillment_order.backordered` ](global-fulfillments.md#backordered-events)event. It notifies you when a product is out of stock. You can handle this event by notifying customers of the delay and providing them the option to cancel the backordered products. If they select this option, submit a [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations).

{% hint style="info" %}
For more information, refer to the [Cancelling physical fulfillments](instructing-digital-to-cancel-items.md) page.
{% endhint %}

#### Responding to product shipment events

In this model, you need to handle [`fulfillment_order.shipped`](global-fulfillments.md#shipped-events) events. The source of these events are shipment notifications sent by the product's fulfiller.

The event's payload informs you which items, and in what quantity, have been shipped to the customer. These shipped events also contain a unique [shipment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments) identifier that allows you to share [tracking information](global-fulfillments.md#tracking-a-shipment) with the customer.

Each time you receive a [`fulfillment_order.shipped`](global-fulfillments.md#shipped-events) event, retrieve its order, product, and shipment data and use it to [define](../../../order-management/informing-digital-river-of-a-fulfillment.md#defining-fulfillments) and [submit](../../../order-management/informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests) a `POST/fulfillments` request. This request instructs Digital River's payment services to [capture](../../../order-management/orders/payment-charges/#captures) the appropriate amount of an [order's](./#assisted-fulfillment-model) payment [charges](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).

#### Responding to product cancellation events

In this model, you also need handle [`fulfillment_order.cancelled`](global-fulfillments.md#cancelled-events) events. The source of these events are either [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations) requests that your system makes or cancellation notifications sent by the product's fulfiller.

The payload of each [`fulfillment_order.cancelled`](global-fulfillments.md#cancelled-events) event informs you which items, and in what quantity, have been cancelled. Each time you receive a cancelled event, retrieve its order and product data, and use it to [define](../../../order-management/informing-digital-river-of-a-fulfillment.md#defining-fulfillments) and [submit](../../../order-management/informing-digital-river-of-a-fulfillment.md#submitting-fulfillment-and-cancellation-requests) a `POST/fulfillments` request. This request instructs Digital River's payment services to [cancel](../../../order-management/orders/payment-charges/#cancels) the appropriate amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment [charges](../../../order-management/orders/payment-charges/).

#### Completing an order

Continue listening for and responding to fulfillment related events. After receiving each event, update the status of the order in your system.

For more information refer to the following sections on the [Capturing and cancelling payment charges](../../../order-management/informing-digital-river-of-a-fulfillment.md) page:

* [Handling charge capture complete and failed events](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-charge-capture-complete-and-failed-events)
* [Handling the charge cancel success event](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-charge-cancel-success-event)
* [Handling the order complete event](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event)

### Orchestrated model

In the orchestrated model, as with all Digital River coordinated fulfillments, your [SKU-inventory item pairs](../../../product-management/common-attributes.md) represent products whose fulfillment Digital River coordinates. In this model, Digital River is responsible for keeping these objects synchronized.

Digital River also handles order accepted, product shipment, and product cancellation events.

The following provides a high-level overview of how you might structure an orchestrated model workflow:

#### Creating and maintaining your product catalog

Prior to deployment, you should build a catalog of [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) whose fulfillment Digital River coordinates. For each product in this catalog, [configure the SKU for Digital River managed fulfillments](../../../product-management/creating-and-updating-skus.md#managed-fulfillments). This configuration results in [SKU-inventory item pairs](../../../product-management/common-attributes.md) whose [shared attribute](../../../product-management/common-attributes.md#shared-attributes) values are synchronized by Digital River.

When [building a checkout](../creating-checkouts/), you can add [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) from your Digital River [managed fulfillment](../../../product-management/creating-and-updating-skus.md#managed-fulfillments) catalog or [digital products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) from other catalogs.

{% hint style="warning" %}
If your site supports the necessary [selling entities](../creating-checkouts/selling-entities.md), then checkouts can also contain [third-party fulfilled physical products](../../../order-management/fulfillments.md#third-party-coordinated-fulfillments).
{% endhint %}

#### Building checkouts and submitting orders

In both this model and the [distributed model](./#distributed-model), you can use the same basic approach to [build your checkouts and submit your orders](./#structuring-checkout-processing-and-order-submissions).

#### How fulfillment of physical products is initiated <a href="#how-physical-product-fulfillment-is-initiated" id="how-physical-product-fulfillment-is-initiated"></a>

In the orchestrated model, once you build the checkout and submit the order, Digital River handles the [`order.accepted` ](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event)event by retrieving data from the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and other upstream resources and using it to submit a [`POST/fulfillment-orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments). This request instructs our fulfillment services to initiate delivery of the order's [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital).

You should handle the[ `order.accepted` event](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders) by updating the status of the order in your commerce platform and by thanking customers for their purchase on an order confirmation page.

#### Responding to product pending and backordered events

If you give customers the option to cancel orders, then the [`fulfillment_order.pending`](global-fulfillments.md#pending-events) event contains the [fulfillment order identifier and fulfillment order line item identifiers](global-fulfillments.md#unique-identifiers) that you need to [create a fulfillment order cancellation](instructing-digital-to-cancel-items.md#requesting-a-fulfillment-cancellation).

You can also subscribe to the [`fulfillment_order.backordered` ](global-fulfillments.md#backordered-events)event. It notifies you when a product is out of stock. You can handle this event by notifying customers of the delay and providing them the option to cancel the backordered products. If they select this option, submit a [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations).

{% hint style="info" %}
For more information, refer to the [Cancelling physical fulfillments](instructing-digital-to-cancel-items.md) page.
{% endhint %}

#### How product shipment events are handled <a href="#product-shipment-events" id="product-shipment-events"></a>

Digital River handles [`fulfillment_order.shipped`](global-fulfillments.md#shipped-events) events emitted by our fulfillment services. The ultimate source of these events are shipment notifications sent by the product's fulfiller.

The payload of each [`fulfillment_order.shipped`](global-fulfillments.md#shipped-events) contains data on which items, and in what quantity, the fulfiller has shipped to the customer. From each shipped event, Digital River retrieves the [order identifier](../../../order-management/creating-and-updating-an-order.md#unique-identifier), [shipment identifiers](global-fulfillments.md#tracking-a-shipment), as well as each line item's identifier and quantity and uses this data to submit an internal request that instructs our payment services to [capture](../../../order-management/orders/payment-charges/#captures) the appropriate amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment [charges](../../../order-management/orders/payment-charges/).

You can listen for [`fulfillment.created`](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-fulfillment-created-event) events generated by this request. These events provide you access to [tracking information](global-fulfillments.md#tracking-a-shipment). Alternatively, you can access this tracking information by subscribing to `fulfillment_order.shipped`.

#### How product cancellation events are handled <a href="#product-cancellation-events" id="product-cancellation-events"></a>

Digital River handles [`fulfillment_cancellation.accepted`](instructing-digital-to-cancel-items.md#responding-to-cancellation-events) events. The source of these events are either [`POST/fulfillment-cancellations`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillmentCancellations) that your system submits or cancellations created by the product's fulfiller.

The payload of each `fulfillment_cancellation.accepted` event contains data on which items, and in what quantity, have been cancelled.

From each event, Digital River retrieves the [order identifier](../../../order-management/creating-and-updating-an-order.md#unique-identifier), the [line item identifier(s)](../../../order-management/creating-and-updating-an-order.md#line-items), and each items' cancelled quantity and uses this data to submit a request that instructs our payment services to [cancel](../../../order-management/orders/payment-charges/#cancels) the appropriate amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment [charges](../../../order-management/orders/payment-charges/).

To be notified when this request is submitted, you can subscribe to the [`fulfillment.created`](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-fulfillment-created-event) event.

#### Completing an order

Continue listening for and responding to fulfillment related events. After receiving each event, update the status of the order in your system.

For more information, refer to the following sections on the [Capturing and cancelling payment charges](../../../order-management/informing-digital-river-of-a-fulfillment.md) page:

* [Handling charge capture complete and failed events](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-charge-capture-complete-and-failed-events)
* [Handling the charge cancel success event](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-charge-cancel-success-event)
* [Handling the order complete event](../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event)

### Building checkouts and submitting orders <a href="#structuring-checkout-processing-and-order-submissions" id="structuring-checkout-processing-and-order-submissions"></a>

In Digital River coordinated fulfillments, both the [distributed model](./#distributed-model) and the [orchestrated model](./#orchestrated-model) allow you to [build checkouts ](./#building-a-checkout)and [submit orders](./#submitting-an-order) using the same basic approach.

{% hint style="info" %}
For more information, refer to [sequencing the checkout process](../creating-checkouts/#sequencing-the-checkout-process) on the [Building checkouts](../creating-checkouts/) page.
{% endhint %}

#### Building a checkout

As customers add items to their carts, you can use the [Inventory Levels API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels) to [display product availability information](checking-inventory-levels.md#using-an-inventory-level) on your storefront.

Once customers have finalized their cart and initiated checkout, send a [create checkout request](../creating-checkouts/#creating-and-updating-the-checkout).

You can then use the checkout's shipping and product data to [request shipping quotes](using-shipping-quotes.md#requesting-shipping-quotes) through the [Shipping Quotes API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes). Use the response to [present shipping options](using-shipping-quotes.md#shipping-quotes) to customers, and then, based on their selection, [update the checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) with a [shipping choice](../creating-checkouts/shipping-choice.md).

Later in the checkout process, you can retrieve the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipTo`, `shippingChoice` and [physical](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) `items[]` and use this data to [make a reservation request](reserving-inventory-items.md#submitting-a-reservation-request) through the [Reservations API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Reservations). If successful, this request places a hold on the product's for the [period of time you designate](reserving-inventory-items.md#expiration-period).

As with every checkout, you must also [create a new payment source](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) or [authenticate an existing payment source](../../../payments/payment-sources/using-the-source-identifier.md#authenticating-sources) and then ensure [one or more sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) are [attached to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

You can then use the [payment session](../creating-checkouts/payment-sessions.md) to determine [when to convert the checkout to an order](../creating-checkouts/payment-sessions.md#how-to-determine-when-to-create-an-order).

#### Submitting an order

You [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) using the [Orders API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). This prompts Digital River to [conduct a fraud review](../../../order-management/orders/the-order-lifecycle.md#fraud-review) and, depending on the results of the payment authorization request, [create a charge](../../../order-management/orders/payment-charges/#how-a-charge-is-created) on each [payment source](../../../payments/payment-sources/).

For next steps:

* If you're using the [distributed model](./#distributed-model), refer to [Initiating physical product fulfillment](./#initiating-physical-product-fulfillment).
* If you're using the [orchestrated model](./#orchestrated-model), refer to [How fulfillment of physical products is initiated](./#how-physical-product-fulfillment-is-initiated)
