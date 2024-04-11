---
description: >-
  Gain a better understanding of the order summary component along with how to
  create and mount it
---

# Order summary component

The order summary component lists the products in the customer's cart at checkout-time and provides an item-level and order-level breakdown of how much they are to be charged, denominated in the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`currency`](../../../digital-river-api-reference/checkout-sessions.md#currency).

For each of that resource's [`items[]`](../../../digital-river-api-reference/checkout-sessions.md#product-data), the component displays its `quantity` along with the `image` and `name` that you either passed in [`productDetails`](../../../../product-management/skus.md#product-details) or stored in the referenced [SKU](../../../../product-management/skus.md#skus).  &#x20;

As customers progress through the various stages of checkout, Digital River computes applicable taxes and shipping costs and then updates the experience. &#x20;

<figure><img src="../../../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

## Creating the order summary component

To create an instance of the order summary component, pass `'ordersummary'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let orderSummaryComponent;
...
orderSummaryComponent = components.createComponent('ordersummary');
```

## Mounting the order summary component

To attach the order summary component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="order-summary-container" style="display: block">
...
orderSummaryComponent.mount('order-summary-container');
```

