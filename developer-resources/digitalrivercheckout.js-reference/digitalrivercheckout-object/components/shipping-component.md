---
description: >-
  Gain a better understanding of the shipping component along with how to create
  and mount it
---

# Shipping component

The shipping component allows customers to select how they want their goods to be shipped.&#x20;

It retrieves [`options.shippingMethods[]`](../../../digital-river-api-reference/checkout-sessions.md#shipping-methods) from the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md), presents these options to customers, prompts them to make a selection, and then uses their input to set the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) `shippingChoice`.&#x20;

<figure><img src="../../../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

To use the shipping component, you'll need to [create it](shipping-component.md#creating-the-shipping-component), [mount it](shipping-component.md#mounting-the-shipping-component), and [submit its data](shipping-component.md#submitting-the-shipping-component). &#x20;

Your application doesn't always need to display this component to customers. In some cases, the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`items[]`](../../../digital-river-api-reference/checkout-sessions.md#product-data) might only contain [digital products](../../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital). Alternatively, customers might have opted to use the [wallet component](wallet-component.md), meaning the customer's shipping method choice is collected within the [payment component](payment-component.md). To determine whether a transaction requires the shipping component, check [`requiresShipping`](configuring-components.md#requiresshipping) in the `data` returned by [`onReady`](configuring-components.md#onready) and [`onChange`](configuring-components.md#onchange).

## Creating the shipping component

To create an instance of the shipping component, pass `'shipping'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let shippingComponent;
...
shippingComponent = components.createComponent('shipping');
```

## Mounting the shipping component

To attach the shipping component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="shipping-container" style="display: block">
...
shippingComponent.mount('shipping-container');
```

## Submitting the shipping component

The shipping component exposes `done()`, which submits the customer's selection and returns a boolean. It requires that you use the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator and, therefore, must be called inside an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function).

```javascript
const shippingComponentStatus = await shippingComponent.done();
```

If `done()` returns `true`, then customers made a selection and the [checkout-sessison's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shippingChoice` has been updated. As a result, you can move the checkout process forward.

If `false`, then don't advance customers to the next stage of the checkout.

