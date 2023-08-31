---
description: >-
  Learn how Source objects created from credit cards function within the
  Commerce API.
---

# Handling credit card sources

In the Commerce API, sources created from credit cards are [multi-use](./#reusable-or-single-use), [synchronous](./#synchronous-or-asynchronous), and [pull-based](./#pull-or-push). This means that customers aren't required to re-enter payment details before every payment, they are provided instant notification of a payment's approval status, and the amount charged to the card can be updated repeatedly throughout the checkout process. &#x20;

The Sources API supports a [wide range of credit cards](./).&#x20;

## Creating a credit card source

To create a credit card source, you must CVCs

## Charging a credit card source

You can either [attach the source to a customer](./#attaching-a-payment-method-to-a-customer) for use in the current checkout and potentially reuse in future payments or [attach it directly to a Cart](using-the-source-identifier.md#attaching-sources-to-a-cart). In the latter case, the source cannot be reused and will have a [state](./#source-state) of `consumed` once charged.&#x20;

{% hint style="danger" %}
Credit card sources should be used shortly after they are created. This is because CVC data expires within a few minutes. Orders created with cards that lack CVCs are more likely to be declined and pose a greater fraud risk.
{% endhint %}

Once you have attached the source to a customer or directly to a cart, Digital River can use it when you [submit the Cart](https://docs.digitalriver.com/commerce-api/cart/submitting-a-cart).
