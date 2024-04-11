---
description: Learn how to set the customer's type during the checkout process.
---

# Setting the customer type

A [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `type` and a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `customerType` allow you to indicate whether the entity making a purchase is a `business` or an `individual`.

When associating a [tax identifier](../../../customer-management/setting-tax-related-attributes.md#tax-identifiers) or [tax certificate](../../../customer-management/setting-tax-related-attributes.md#tax-certificates) to a checkout, you typically indicate the purchaser is a `business`. For more information about exceptions to this rule, refer to the [supported tax identifiers](tax-identifiers.md#supported-tax-identifiers) section on the [Tax identifiers](tax-identifiers.md) page.

## Including a business customer's organization

When [registered](using-the-checkout-identifier.md#registered-checkouts-or-invoices) and [guest](using-the-checkout-identifier.md#guest-checkouts-or-invoices) `business` customers are making a purchase, you should specify their organization by setting:

* The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipTo.organization` when providing a customer's [shipping information](providing-address-information.md#ship-to-address).
* The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `billTo.organization` when providing a customer's [billing information](providing-address-information.md#bill-to-address).
