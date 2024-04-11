---
description: >-
  Learn how Source objects created from credit cards function within the Digital
  River API.
---

# Handling credit card sources

In the Digital River API, sources created from credit cards are [multi-use](./#reusable-or-single-use), [synchronous](./#synchronous-or-asynchronous), and [pull-based](./#pull-or-push). This means that customers aren't required to re-enter payment details before every payment; they are provided instant notification of a payment's approval status, and the amount charged to the card can be updated repeatedly throughout the checkout process.

The Sources API supports a [wide range of credit cards](./#payment-methods).

## Creating a credit card source

To ensure that you remain PCI compliant, credit card Source objects are [created by DigitalRiver.js](../payment-integrations-1/digitalriver.js/quick-start.md#step-1-include-digitalriver-js-on-your-page) and then returned to your integration.

You must [include the DigitalRiver.js library](../payment-integrations-1/digitalriver.js/quick-start.md#step-1-include-digitalriver-js-on-your-page) on your payment collection form to create a credit card source. You then [create your payment form](../payment-integrations-1/digitalriver.js/quick-start.md#step-2-create-your-payment-form) and [embed elements](../payment-integrations-1/digitalriver.js/quick-start.md#step-3-create-and-embed-elements) on it. Once a customer has supplied payment details, you pass the data to DigitalRiver.js to [create the payment source](../payment-integrations-1/digitalriver.js/quick-start.md#step-4-use-digitalriver-js-to-create-a-payment-source). We then return a source identifier to your integration.

## Charging a credit card source

You can either [attach the Source to a Customer](using-the-source-identifier.md#attaching-sources-to-customers) for use in the current Checkout and potentially reuse it in future payments or [attach it directly to a Checkout](using-the-source-identifier.md#attaching-sources-to-checkouts). In the latter case, the Source cannot be reused and will have a [state](./#source-state) of `consumed` once charged.

{% hint style="danger" %}
Credit card sources should be used shortly after they are created. This is because CVC data expires within a few minutes. Orders created with cards that lack CVCs are more likely to be declined and pose a greater fraud risk.
{% endhint %}

Once you have attached the Source to a Customer or directly to a Checkout, Digital River can then use it to create a [Charge object](../../developer-resources/digital-river-api-reference/payment-charges.md) when you [submit an Order](../../order-management/creating-and-updating-an-order.md).
