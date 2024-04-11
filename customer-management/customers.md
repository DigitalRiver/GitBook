---
description: Learn about the customer resource
---

# Customer basics

A [customer resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) allows you to store a customer's unique identifier, name, phone, email, shipping address, saved payment sources, tax identifiers, tax certificates and other data.

This resource is especially useful in [registered checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices).

For example, once you set a customer's `shipping.address`, you can retrieve these values during later [checkouts](../integration-options/checkouts/creating-checkouts/) and display them as an available option to the storefront customer. This often helps expedite the checkout process.

Additionally, if customers want to save a [reusable payment method](../payments/supported-payment-methods/) for future use, you can [attach the created payment source to their record](../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers). When that same customer later initiates a [registered checkout](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices), you can [retrieve a list of applicable payment methods](../developer-resources/reference/digitalriver-object.md#retrieving-available-payment-methods) and then use this list to filter the customer's [reusable sources](../payments/payment-sources/#reusable-or-single-use) before displaying them in your GUI.

You can also use the resource to [set up and store a customer's tax exempt data](setting-tax-related-attributes.md).
