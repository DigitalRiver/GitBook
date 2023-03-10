---
description: >-
  Learn how source objects created from credit cards function within the
  Commerce API.
---

# Handling credit card sources

In the Commerce API, sources created from credit cards are [multi-use](./#reusable-or-single-use), [synchronous](./#synchronous-or-asynchronous), and [pull-based](./#pull-or-push).  This means that customers aren't required to re-enter payment details before every payment, they are provided instant notification of a payment's approval status, and the amount charged to the card can be updated repeatedly throughout the checkout process. &#x20;

The [Sources API](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source) supports a [wide-range of credit cards](./#payment-methods).&#x20;

## Creating a credit card source

To ensure that you remain PCI compliant, credit card Source objects are [created by DigitalRiver.js](../payments-solutions/digitalriver.js/quick-start.md#step-4-use-digitalriver-js-to-create-a-payment-source) and then returned to your integration.&#x20;

To create a credit card source, you must first [include the DigitalRiver.js library](../payments-solutions/digitalriver.js/quick-start.md#step-1-include-digitalriver-js-on-your-page) on your payment collection form. You then [create your payment form](../payments-solutions/digitalriver.js/quick-start.md#step-2-create-your-payment-form) and [embed elements](../payments-solutions/digitalriver.js/quick-start.md#step-3-create-and-embed-elements) on it. Once a customer has supplied payment details, you pass the data to DigitalRiver.js to [create the payment source](../payments-solutions/digitalriver.js/quick-start.md#step-4-use-digitalriver-js-to-create-a-payment-source). We then return a source identifier to your integration.&#x20;

## Charging a credit card source

You can either [attach the source to a customer](./#attaching-a-payment-method-to-a-customer) for use in the current checkout and potentially reuse in future payments or [attach it directly to a Cart](using-the-source-identifier.md#attaching-sources-to-a-cart). In the latter case, the source cannot be reused and will have a [state](./#source-state) of `consumed` once charged.&#x20;

{% hint style="danger" %}
Credit card sources should be used shortly after they are created. This is because CVC data expires within a few minutes. Orders created with cards that lack CVC's are more likely to be declined and pose a greater fraud risk.
{% endhint %}

Once you have attached the source to a customer or directly to a cart, it can then be used by Digital River when you [submit the Cart](../../shopper-apis/cart/submitting-a-cart/).
