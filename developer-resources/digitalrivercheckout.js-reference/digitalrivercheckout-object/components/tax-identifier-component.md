---
description: >-
  Gain a better understanding of the tax identifier component, how to create and
  mount it, as well as how to submit the information it collects
---

# Tax identifier component

The tax identifier component can collect a customer's tax identification number.&#x20;

To use the component, you'll need to [create it](tax-identifier-component.md#creating-the-tax-identifier-component), [mount it](tax-identifier-component.md#mounting-the-tax-identifier-component), and [submit its data](tax-identifier-component.md#submitting-the-tax-identifier-component).

The following are some of the following types of tax identifiers the component collects:

{% tabs %}
{% tab title="VAT" %}
When the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type) is `business` and the customer's country is Germany, the component collects a Value Added Tax (VAT) number.

<figure><img src="../../../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="GST" %}
When the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type) is `business` and the customer's country is Canada, the component collects a Goods and Services Tax (GST) identifier.

<figure><img src="../../../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="UBN" %}
When the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type) is `business` and the customer's country is Taiwan, the component collects a Unified Business Number (UBN).

<figure><img src="../../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="RFC" %}
When the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type) is `business` and the customer's country is Mexico, the tax component collects a Registro Federal de Contribuyentes (RFC) number.

<figure><img src="../../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

If your site sells outside the United States, particularly in the European Union, you'll likely need to implement the tax identifier component. This is especially true if you allow customers to make purchases on behalf of a business entity (i.e., B2B transactions).

{% hint style="info" %}
If you know, before sending the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), whether customers are making the purchase as an individual or on behalf of a business, you can define [`customerType`](../../../digital-river-api-reference/checkout-sessions.md#customer-type). Alternatively, by using the [auto-collect customer type](../../../digital-river-api-reference/checkout-sessions.md#auto-collect-customer-type) feature, you can configure the address component to get this information from customers
{% endhint %}

In some countries, customers must enter a tax identification number when making an e-commerce purchase. To access a list of these countries, refer to [Supported tax identifiers](../../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers).&#x20;

In the `data` returned by [`onReady`](configuring-components.md#onready), you can use [`showTaxIdentifiers`](configuring-components.md#showtaxidentifiers) to determine whether the component must be displayed. Additionally, [`onChange`](configuring-components.md#onchange) allows you to determine when it's optional and required.&#x20;

Once customers input a properly formatted value, Digital River creates a [tax identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers) and associates that object with the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions). After the customer successfully makes payment and completes their purchase, Digital River adds that same `taxIdentifiers[]` to the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

You should be aware, however, that a [tax identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers) won't affect how an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) taxes are calculated unless its [`state`](../../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#states-and-triggered-events) is `pending` or `verified`. For details, refer to [How we validate tax identifiers](../../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#how-we-validate-tax-identifiers). &#x20;

## Creating the tax identifier component

To create an instance of the tax identifier component, pass `'taxidentifier'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let taxIdentifierComponent;
...
taxIdentifierComponent = components.createComponent('taxidentifier');
```

## Mounting the tax identifier component

To attach the tax identifier component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="tax-identifier-container" style="display: block"></div>
...
taxIdentifierComponent.mount('tax-identifier-container');
```

## Submitting the tax identifier component

The tax identifier component exposes `done()`, which submits the customer's input and returns a boolean. It requires that you use the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator and, therefore, must be called inside an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function).

```javascript
const taxIdentifierComponentStatus = await taxIdentifierComponent.done();
```

If `done()` returns `true`, then this indicates that (1) customers entered a properly formatted value and Digital River used it to create a [tax identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers) and associate that object with the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) or (2) customers entered an improperly formatted value (or nothing at all) but they're shopping in a country that gives them the option to supply a tax id number when making an e-commerce purchase but doesn't require it.&#x20;

If `true`, your code can advance customers to the next stage in checkout. &#x20;

A `false` value indicates that (1) the customer's country requires a tax id number to make the purchase and (2) customers either didn't provide a value or it's incorrectly formatted, and, as a result, Digital River cannot create a [tax identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers).&#x20;

If `false`, your application should contain logic that prevents customers from advancing to the next stage in the checkout. &#x20;

In this case, the component prompts customers to re-enter a value and typically offers formatting assistance.

{% tabs %}
{% tab title="VAT" %}
Example help text displayed when the customer's country is Germany, and they're checking out as a business entity.

<figure><img src="../../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="UBN/TIN" %}
Example help text displayed when the customer's country is Taiwan, and they're checking out as a business entity.

<figure><img src="../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="RFC" %}
Example help text displayed when the customer's country is Mexico, and they're checking out as a business entity.

<figure><img src="../../../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
