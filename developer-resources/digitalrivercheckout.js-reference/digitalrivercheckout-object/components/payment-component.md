---
description: Learn how to accept payment in a secure, customizable component
---

# Payment component

The payment component displays transaction-applicable payment methods and then processes the customer's selection.&#x20;

{% hint style="info" %}
For a list of payments the component supports, refer to [Supported payment methods](../../../../payments/supported-payment-methods/).
{% endhint %}

Unless your checkout only uses the [wallet component](wallet-component.md) (plus the mandatory [compliance component](compliance-component.md)), you'll need to implement this component.

To use [the component's features](payment-component.md#features), you'll need to [create it](payment-component.md#creating-the-payment-component) and [mount it](payment-component.md#mounting-the-payment-component).&#x20;

## Features

After customers make a selection, the payment component can, when necessary, redirect customers to payment providers and handle [PSD2/SCA](../../../../payments/psd2-and-sca/) requirements.&#x20;

The component also has the capability to:

* [Present saved payment methods](payment-component.md#saved-payment-options)
* [Save payment methods for future purchases](payment-component.md#save-a-payment-method-for-future-purchases)&#x20;
* [Display customized consents](payment-component.md#custom-consents)

### Saved payment options

The component can display a customer's saved payment methods for convenience purposes.

To activate this feature, you need to pass [`customerId`](../../../digital-river-api-reference/checkout-sessions.md#customer-identifier) in the [create checkout session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession). Digital River then determines whether the referenced [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) exists, and, if it does, retrieves and displays its transaction-applicable payment [`sources[]`](../../../../payments/payment-sources/).



<figure><img src="../../../../.gitbook/assets/saved payment methods.png" alt=""><figcaption></figcaption></figure>

### Save a payment method for future purchases

The component can ask customers whether they'd like to save a payment method for future purchases.&#x20;

To activate this feature, you must pass [`customerId`](../../../digital-river-api-reference/checkout-sessions.md#customer-identifier) in the [create checkout session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

{% hint style="info" %}
If the referenced resource doesn't exist in your account, Digital River creates a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers). &#x20;
{% endhint %}

If the payment method selected by customers supports [reusability](../../../../payments/payment-sources/#reusable-or-single-use), then the component asks whether they'd like to save it for future purchases. If customers opt to do so, then, after Digital River creates the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), we save it to that [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).&#x20;

### Custom consents

For each payment method that the component displays, customers are shown the terms of sale and the privacy policy of the transaction's designated [selling entity](../../../../integration-options/checkouts/creating-checkouts/selling-entities.md).

If you [save your consents in Digital River Dashboard](../../../../administration/dashboard/settings/prebuilt-checkout.md), they are appended to Digital River's disclosures.&#x20;

The component requires customers to accept all of these terms before they can complete the purchase. &#x20;

{% hint style="info" %}
To [determine what disclosures customers accepted](../../../../integration-options/low-code-checkouts/handling-completed-checkout-sessions.md#determine-what-disclosures-customers-accepted), you can [configure a webhook](../../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../../../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../../../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).
{% endhint %}

{% tabs %}
{% tab title="Digital River only disclosures" %}
If you have no [customized consents in Dashboard](../../../../administration/dashboard/settings/prebuilt-checkout.md), the component only displays Digital River's disclosures.

<figure><img src="../../../../.gitbook/assets/no appended consents.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Combined disclosures" %}
If you [add consents in Dashboard](../../../../administration/dashboard/settings/prebuilt-checkout.md), the component displays your disclosures and ours.

<figure><img src="../../../../.gitbook/assets/appended consents (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Creating the payment component

To create an instance of the payment component, pass `'payment'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let paymentComponent;
...
paymentComponent = components.createComponent('payment');
...
```

## Mounting the payment component

To attach the payment component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).&#x20;

```javascript
<div id="payment-container" style="display: block">
...
paymentComponent.mount('payment-container');
...
```
