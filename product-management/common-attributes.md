---
description: >-
  Learn about how to use SKU-inventory items pairs in Digital River coordinated
  fulfillments
---

# SKU-inventory item pairs

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), your [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) and [inventory items](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) form synchronized pairs. While [building checkouts](../integration-options/checkouts/creating-checkouts/), [processing orders](../order-management/creating-and-updating-an-order.md), and [fulfilling goods](../order-management/fulfillments.md), their [shared attributes](common-attributes.md#shared-attributes) must remain synchronized.

This allows these resources to be used interchangeably during order processing and product fulfillment.

How you create these pairs and maintain this synchronicity depends on whether you're using the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model) or the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model).

In the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), Digital River automates the synchronization process. All you have to do is [configure the SKU's `managedFulfillment` ](creating-and-updating-skus.md#managed-fulfillments)attribute. In the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model), you are responsible for maintaining data consistency between your SKU-inventory item pairs.

## Shared attributes

[SKUs](skus.md#skus) and [inventory items](skus.md#inventory-items) share certain attributes. In both resources, you can set its identifier, country of origin, export control classification number, manufacturer identifier, part number, and Harmonized System code. You can also indicate whether a product can be oversold.

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), these common attributes must remain harmonized. How that harmonization is achieved, depends on whether you're using the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model) or the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model).

Use the links in the following table to be directed to the resource specific documentation for each attribute.

| SKUs                                                                              | Inventory items                                                                   |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [`id`](creating-and-updating-skus.md#unique-identifier)                           | [`id`](managing-inventory.md#unique-identifier)                                   |
| [`manufacturerId`](creating-and-updating-skus.md#manufacturer-id-and-part-number) | [`manufacturerId`](managing-inventory.md#manufacturer-identifier-and-part-number) |
| [`partNumber`](creating-and-updating-skus.md#manufacturer-id-and-part-number)     | [`partNumber`](managing-inventory.md#manufacturer-identifier-and-part-number)     |
| [`countryOfOrigin`](creating-and-updating-skus.md#country-of-origin)              | [`countryOfOrigin`](managing-inventory.md#country-of-origin)                      |
| [`eccn`](creating-and-updating-skus.md#eccn)                                      | [`eccn`](managing-inventory.md#eccn)                                              |
| [`hsCode`](creating-and-updating-skus.md#harmonized-system-code)                  | [`hsCode`](managing-inventory.md#harmonized-system-code)                          |
| [`allowOversell`](creating-and-updating-skus.md#allow-oversell)                   | [`allowOversell`](managing-inventory.md#allow-oversell)                           |
