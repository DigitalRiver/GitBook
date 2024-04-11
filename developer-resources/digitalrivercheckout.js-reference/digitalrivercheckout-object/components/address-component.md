---
description: >-
  Gain a better understanding of the address component, how to create and mount
  it, as well as how to submit the information it collects from customers
---

# Address component

The address component collects a customer's shipping and/or billing information.&#x20;

For many countries, the component:

* Presents customers with a list of acceptable political subdivisions, such as states and provinces, and then requires that they make a selection.
* Validates the format of a customer's postal code.

To successfully use the component, you'll need to [create it](address-component.md#creating-the-address-component), [mount it](address-component.md#mounting-the-address-component), and [submit its data](address-component.md#submitting-the-address-component).

In most cases, you'll need to implement this component. This is true whether your site sells physical and/or digital products. However, if your application only uses the [wallet component](wallet-component.md) (plus the mandatory [compliance component](compliance-component.md)), you might not have any need for it.&#x20;

Once the component gathers and (in some cases) validates a customer's input, Digital River uses it to set the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) `shipTo` and/or `billTo`.

What inputs that the component requires and what options it presents, depends on whether the checkout involves:

* [Physical and/or digital products](address-component.md#digital-and-physical-products)
* [Registered customers](address-component.md#registered-customers)
* [Customers conducting a B2B transaction](address-component.md#business-to-business-transactions)

## Digital and physical products

Whether the address component collects shipping and/or billing information depends on [`items[]`](../../../digital-river-api-reference/checkout-sessions.md#product-data) in the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md). If any represent a [physical product](../../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), then the component prompts customers for their shipping address and gives them the option to enter a different billing address.

If all the `items[]` are [digital](../../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), then it only collects billing information.&#x20;

{% tabs %}
{% tab title="Checkouts with physical products" %}
<figure><img src="../../../../.gitbook/assets/billing address.png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Checkouts with only digital products" %}
<figure><img src="../../../../.gitbook/assets/image (108).png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Registered customers

If you define [`options.addresses[]`](../../../digital-river-api-reference/checkout-sessions.md#saved-addresses), the component presents these saved addresses to users for convenience.

{% tabs %}
{% tab title="Saved addresses" %}
<figure><img src="../../../../.gitbook/assets/image (136).png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Business to business transactions

If you activate the [auto collect customer type ](../../../digital-river-api-reference/checkout-sessions.md#auto-collect-customer-type)feature, the component displays a checkbox that asks customers whether they’d like to purchase on behalf of a business.

If customers select this option or you pass a [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type) of `business` , customers must provide their company's name when entering shipping and billing information.

<figure><img src="../../../../.gitbook/assets/image (120).png" alt="" width="375"><figcaption></figcaption></figure>

## Creating the address component

To create an instance of the address component, pass `'address'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let addressComponent;
...
addressComponent = components.createComponent('address');
```

## Mounting the address component

To attach the address component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="address-container" style="display: block">
...
addressComponent.mount('address-container');
```

## Submitting the address component

The address component exposes `done()`, which submits the form and returns a boolean. The function requires the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator and, therefore, must be called inside an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function).

```javascript
const addressComponentStatus = await addressComponent.done();
```

The value returned by the function indicates whether the customer's shipping and/or billing information is complete, valid, and added to the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shipTo` and/or `billTo`.&#x20;

If `true`, then your application can move on to the next stage in the checkout.

If `false`, Digital River determined that either the address is invalid (most likely because customers entered an incorrectly formatted postal code or email address) or customers failed to enter the required information.

{% hint style="success" %}
For certain fields, the address component supplies customers with tips on how to format their input.&#x20;
{% endhint %}

If `false`, make sure you implement logic that blocks the checkout from advancing to the next stage. In other words, the address component should remain displayed to customers.
