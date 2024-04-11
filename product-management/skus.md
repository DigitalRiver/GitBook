---
description: Learn the basics of SKUs, product details, SKU groups, and inventory items.
---

# Product basics

In the Digital River APIs, you can use [SKUs](skus.md#skus), [product details](skus.md#product-details), [SKU groups](skus.md#sku-groups) and [inventory items](skus.md#inventory-items) to identify and describe your goods and services.

Whether you integrate with [Low-code checkouts](../integration-options/low-code-checkouts/) or [Direct Integrations](../integration-options/checkouts/), these resources and objects allow you to define each of your product's [basic and compliance data](skus.md#basic-versus-compliance-product-data).

Except for [SKU groups](skus.md#sku-groups) (as well as [inventory items](skus.md#inventory-items) used in the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model) of [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/)), you're responsible for managing the data contained in them.

Additionally, with the exception of [product details](skus.md#product-details), their data is stored in Digital River's system.

|                                                | Resource or object? | Supported product data | Where the product data is stored | Who manages the product data | How you manage the data                                                                                   | When you reference the resource / pass the object                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------------- | ------------------- | ---------------------- | -------------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**SKUs**](skus.md#skus)                       | Resource            | Basic and compliance   | Digital River's system           | You                          | [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs)                       | [`POST /checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts), [`POST /checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession)                                                                                                                                                                                                                                                                                                                                                                                            |
| [**Product details**](skus.md#product-details) | Object              | Basic                  | Your system                      | You                          | System dependent                                                                                          | <p><a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts"><code>POST /checkouts</code></a>, <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession"><code>POST /checkout-sessions</code></a>, <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes/operation/postShippingQuotes"><code>POST /shipping-quotes</code></a>,<br><a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel"><code>POST /shipping-labels</code></a></p> |
| [**SKU groups**](skus.md#sku-groups)           | Resource            | Compliance             | Digital River's system           | Digital River                | [SKU Groups API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups)            | <p><a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts"><code>POST /checkouts</code></a>, <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession"><code>POST /checkout-sessions</code></a>, <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes/operation/postShippingQuotes"><code>POST /shipping-quotes</code></a>,<br><a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel"><code>POST /shipping-labels</code></a></p> |
| [**Inventory items**](skus.md#inventory-items) | Resource            | Basic and compliance   | Digital River's system           | You/Digital River            | [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) | [`POST /fulfillment-orders`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Orders/operation/createFulfillmentOrders)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## SKUs

In the Digital River APIs, [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) are one option you have to identify and define your goods and services.

This resource holds data on the most important characteristics of a product. SKUs aren’t meant to be universal. Instead, they should be unique to your business.

You [manage SKUs](creating-and-updating-skus.md) and their data is stored in Digital River's system.

Depending on how you send product data in [create checkout](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) or [create checkout-session](../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) requests, your SKUs might only contain [basic product data](skus.md#basic-versus-compliance-product-data). Alternatively, they can contain both [basic and compliance data](skus.md#basic-versus-compliance-product-data).

If you reference this resource in [checkouts ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts)or [checkout-sessions](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions), then you'll need to use the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) to define and create a SKU for every [digital and physical product](skus.md#how-products-are-classified-as-physical-or-digital) in your catalog.&#x20;

For more details, refer to:

* The [Managing SKUs](creating-and-updating-skus.md) page
* The [Sending product data in checkouts](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items](../integration-options/checkouts/creating-checkouts/describing-the-items/) page
* The [Product data](../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) section on the [Checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md) page.&#x20;

## Product details

You can use `productDetails` to identify and define your goods and services. This object holds data on the most important characteristics of a product.

You manage `productDetails` and its data is stored in your system.

A `productDetails` object can only be used to pass [basic product data](skus.md#basic-versus-compliance-product-data). Its [compliance data](skus.md#basic-versus-compliance-product-data) is stored in a referenced [SKU group](setting-up-sku-groups.md).

In other words, each `items[]` in a [create checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [create checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession) request must include `productDetails` and nested within that object should be a `skuGroupId`.

For more details, refer to:

* The [Using product details](using-product-details.md) page
* The [Grouping SKUs](setting-up-sku-groups.md) page
* The [Sending product data in checkouts](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items](../integration-options/checkouts/creating-checkouts/describing-the-items/) page
* The [Product data](../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) section on the [Checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md) page

## SKU groups

A [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) represents a collection of products with similar compliance requirements. This resource is only used to store [compliance data](skus.md#basic-versus-compliance-product-data).

Digital River manages your SKU groups, and their data is stored in Digital River's system.&#x20;

If you use SKU groups, you must reference the resource when sending product data in [create checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [create checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession) requests and the reference must either be in the [SKU](skus.md#skus) or in [`productDetails`](skus.md#product-details).

For more details, refer to:

* The [Grouping SKUs](setting-up-sku-groups.md) page
* The [sending product data in checkouts](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items](../integration-options/checkouts/creating-checkouts/describing-the-items/) page
* The [Product data](../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) section on the [Checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md) page

## Inventory items

The [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) resource identifies and defines physical products stored in a warehouse. You only use inventory items in [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/).

An inventory item's data is saved in Digital River's system and you access it by using the [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items).

How you [interact with inventory items](managing-inventory.md) and how you ensure that data contained in the [shared attributes](common-attributes.md#shared-attributes) of [SKU-inventory item pairs](common-attributes.md) remains synchronized, depends on whether you're using the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model) or the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model).

For more details, refer to:

* The [Managing inventory items](managing-inventory.md) page
* The [SKU-inventory item pairs](common-attributes.md) page

## Basic versus compliance product data

In the Digital River APIs, there exists two broad categories of product data: basic and compliance. The following table lists the specific data in each category:

{% hint style="info" %}
Additional compliance data, beyond what is listed here, may be stored in the [SKU group](setting-up-sku-groups.md#product-compliance-data-in-sku-groups) that a product belongs to.
{% endhint %}

| Basic product data                      | Compliance product data              |
| --------------------------------------- | ------------------------------------ |
| Name and description                    | Export control classification number |
| Image and URL                           | Harmonized system code               |
| Weight and weight unit                  | Tax code                             |
| Country of origin                       | Dangerous goods classifications      |
| Part number and manufacturer identifier | Signature requirements               |

## How products are classified as physical or digital

Digital River classifies a product as either physical or digital based on its designated tax code. This code plays a role in determining a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [address requirements](../integration-options/checkouts/creating-checkouts/providing-address-information.md#address-requirements-and-validations), its assigned [selling entity](../integration-options/checkouts/creating-checkouts/selling-entities.md), and whether the [landed cost feature](../integration-options/checkouts/creating-checkouts/landed-costs.md) is triggered.

Who assigns a product's tax code depends on whether or not you're using SKU groups.

### Using SKU groups

If you (1) associate a [SKU group](skus.md#sku-groups) with each of your [SKUs](skus.md#skus) or (2) reference a [SKU group](skus.md#sku-groups) in [`productDetails`](skus.md#product-details), then Digital River sets the SKU group's tax code.

As a result, you're not responsible for identifying, defining, or managing your products' tax codes.

### Not using SKU groups

If you use [SKUs](skus.md#skus) without [SKU groups](skus.md#sku-groups), then you're responsible for defining and managing each of your SKUs' [`taxCode`](creating-and-updating-skus.md#tax-code)(s).

### How to identify a physical or digital SKU

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/retrieveSkus) `physical` attribute allows you to determine whether the resource is classified as digital or physical without having to reference our [supported tax code table](creating-and-updating-skus.md#supported-tax-codes).

{% code title="SKU" %}
```javascript
{
    "id": "db148281-a5a2-4349-baf2-5d9f76025e56",
    ...
    "physical": true
}
```
{% endcode %}
