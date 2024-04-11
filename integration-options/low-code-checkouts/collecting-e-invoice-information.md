---
description: >-
  Learn how to use a low-code checkout to comply with e-invoicing requirements
  in Taiwan
---

# Collecting e-invoice information

By pairing one of Digital River's [low-code checkout solutions](./) with our [e-invoicing service](../../using-our-services/e-invoicing.md), you can make domestic sales in Taiwan that comply with that country's data collection requirements.

On this page, you'll find information on:

* [Defining ship from](collecting-e-invoice-information.md#defining-ship-from)
* [Determining customer type](collecting-e-invoice-information.md#determining-customer-type)
* [How the invoice collection process works in Prebuilt Checkout](collecting-e-invoice-information.md#invoice-collection-in-prebuilt-checkout)
* [How to collect e-invoicing information in Components](collecting-e-invoice-information.md#how-to-collect-e-invoicing-information-in-components)

## Defining ship from

If [`items[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) in your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) contain [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), there's a variety of [ways to define `shipFrom`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#ship-from). However, to collect carrier information from customers making the purchase as an individual, the value of `shipFrom` must be `TW`.

## Determining customer type

To collect the appropriate information from customers, Digital River needs to know whether they're making the purchase as an individual or on behalf of an organization. If you know this information before initiating checkout, you can define [`customerType`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-type) in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession). Alternatively, you can [configure the checkout-session so that Digital River collects this information](../../developer-resources/digital-river-api-reference/checkout-sessions.md#auto-collect-customer-type). &#x20;

## Invoice collection in Prebuilt Checkout

Prebuilt Checkout determines whether it's a [business-to-customer](collecting-e-invoice-information.md#b2c) or [business-to-business](collecting-e-invoice-information.md#b2b) transaction and then collects the appropriate information.&#x20;

### B2C

If [`customerType`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-type) is `individual` and customers use Prebuilt Checkout's drop-down menu to select Taiwan as their shipping or billing country (or you pass a [`shoppingCountry`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#shopping-country) of `TW` in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession)), Digital River collects and validates the customer's carrier information.

<figure><img src="../../.gitbook/assets/B2C Taiwan.png" alt=""><figcaption></figcaption></figure>

### B2B

If [`customerType`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-type) is `business` and customers use the Prebuilt Checkout's drop-down menu to select Taiwan as their shipping or billing country (or you pass a [`shoppingCountry`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#shopping-country) of `TW` in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession)), Digital River collects and validates the customer's tax identification number.

<figure><img src="../../.gitbook/assets/B2B Taiwan.png" alt=""><figcaption></figcaption></figure>

## How to collect e-invoicing information in Components

In [Component checkouts](implementing-a-components-checkout.md), you'll need to use the data sent by callback functions to determine what information to collect from customers.&#x20;

If  [`showTaxIdentifiers`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#showtaxidentifiers) is `true` in [`onReady`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#ready-event) or `requiredTaxIdentifiers[]` exists in [`onChange`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#change-event), then the customer is making the purchase on behalf of a business entity. As a result, you'll need to display the [tax identifier component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md).&#x20;

If [`showInvoiceAttribute`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#showinvoiceattribute) exists in `onChange` and its value is `true`, then the customer is making the purchase an individual. As a result, you'll need to display the [invoice component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/invoice-component.md).&#x20;

In both cases, when customers attempt to advance to the checkout's next stage by clicking your forward navigation control, call the applicable component's `done()` function and then check the value it returns to determine whether the input is valid and the process can advance.&#x20;

For details, refer to:

* [Submitting the tax identifier component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md#submitting-the-tax-identifier-component)
* [Submitting the invoice attribute component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/invoice-component.md#submitting-the-invoice-component)

