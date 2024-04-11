---
description: Tap into these use cases when developing and testing your commerce connector.
---

# Test and use cases

Here you'll find a continually expanding list of use cases that you can use when developing and testing your commerce connector. You can also reference our [sequence diagram](integration-checklists/#sequence-diagram) to better understand how these use cases fit into the lifecycle of a Digital River order.

## Create a physical SKU

The commerce connector uses the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) to create a [physical SKU](../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital). This allows Digital River to [compute taxes](../../integration-options/checkouts/creating-checkouts/tax-calculations.md) and return that information to customers during the checkout process.

## Create a digital SKU

The commerce connector uses the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) to create a [digital SKU](../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital). This allows Digital River to [compute taxes](../../integration-options/checkouts/creating-checkouts/tax-calculations.md) and return that information to customers during the checkout process.

## Create a checkout as a guest customer

The commerce connector uses the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) to create a [guest checkout](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#guest-checkouts-or-invoices). This means the customer isn't required to create an account during the checkout process.

## Create a checkout as a registered customer

The commerce connector uses the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) to create a [registered checkout](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices). This means customers aren't required to reenter their shipping, billing, and payment details during the checkout process.
