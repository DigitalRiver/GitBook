---
description: Gain a better of how to create express checkouts using the wallet component
---

# Wallet component

The wallet component allows customers to initiate an express checkout using any of the following payment methods:&#x20;

* [PayPal](../../../../payments/supported-payment-methods/paypal.md)
* [Apple Pay](../../../../payments/supported-payment-methods/apple-pay.md)
* [Google Pay](../../../../payments/supported-payment-methods/google-pay.md)

<figure><img src="../../../../.gitbook/assets/express checkout.png" alt=""><figcaption></figcaption></figure>

When customers click any of the component's buttons, they're redirected to that payment provider's interface. There they designate a shipping and/or billing address, select a payment method and then authorize it. If payment is successfully authorized, customers are sent back to your site, and Digital River adds the customer's payment [`sources[]`](../../../../payments/payment-sources/), `shipTo`, and/or `billTo` to the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md).

{% hint style="warning" %}
Certain browsers don't support some express payment methods. For example, the wallet component doesn't render Apple Pay in Chrome.
{% endhint %}

If customers initiate an express checkout, and [`items[]`](../../../digital-river-api-reference/checkout-sessions.md#product-data) in the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md) contains [physical products](../../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), then the customer's shipping method selection is collected within the [payment component](payment-component.md). As a result, if the transaction involves physical products and you're using the wallet component, your application needs to implement the payment component.

## Creating the wallet component

To create an instance of the wallet component, pass `'wallet'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let walletComponent;
...
walletComponent = components.createComponent('wallet');
...
```

## Mounting the wallet component

To attach the wallet component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="wallet-container" style="display: block">
...
walletComponent.mount('wallet-container');
...
```
