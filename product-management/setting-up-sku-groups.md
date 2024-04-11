---
description: >-
  Understand the purpose of SKU groups as well as how they're defined, managed,
  and associated with products
---

# Grouping SKUs

A [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) represents a collection of products with similar compliance requirements. SKU groups store [product compliance data](setting-up-sku-groups.md#product-compliance-data-in-sku-groups) so that it can be used when calculating taxes, determining landed cost, identifying goods at international borders, creating invoices, and numerous other downstream operations.

## Product compliance data in SKU groups

Tax codes, export control classification numbers, dangerous goods handling requirements, and delivery confirmation requirements is just some of the [product compliance data](skus.md#basic-versus-compliance-product-data) that is held in [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups).

## Why use SKU groups?

You can use [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) to:

* [Reduce your product compliance burdens](setting-up-sku-groups.md#reduce-compliance-burdens)
* [Simplify catalog management](setting-up-sku-groups.md#simplify-catalog-management)
* [Open new markets](setting-up-sku-groups.md#open-new-markets)

### Reduce compliance burdens

[SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) minimize the complexity of product compliance. With SKU groups, you're no longer solely responsible for researching and defining product data.

When you use this resource, you don't have to know your product's tax code, country specific tariff codes, and other arcane data. Digital River uses its product classification services to help you identify these values.

### Simplify catalog management

[SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) can also simplify the process of managing product data.

If you decide to [use product details](using-product-details.md) and SKU groups in [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [checkout-sessions](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions), then you don't have to persist any [basic product data](skus.md#basic-versus-compliance-product-data) in Digital River's system.

Instead, at run-time, you simply retrieve this basic product data from your system and send it to us. This means you're not required to keep product catalogs in your system synchronized with [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) data in our system.

### Open new markets

[SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) allow you to open new markets with less effort.

As Digital River adds [product compliance fields](skus.md#basic-versus-compliance-product-data) to the SKU group resource, you can use the data contained in these fields to access new markets. In other words, your application continues sending the same [basic product data](skus.md#basic-versus-compliance-product-data) in [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [checkout-sessions](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession). But, due to internal modifications made to the SKU group by Digital River, your products become compliant in new markets.

Similarly, new data added to existing SKU group fields can also be used to open markets.

#### Example one

At some point, Digital River identifies [product compliance data](skus.md#basic-versus-compliance-product-data) that is needed to ship goods into Indonesia. If this is a market opportunity you're interested in pursuing, we can add this data to your [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups).

After that, whenever a customer in Indonesia makes a purchase on your site, this new compliance data is passed downstream to the appropriate logistics services.

#### Example two

Your [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) may currently configure your products for sale into ten different countries. At some point, however, you identify another country that you'd like to export your products to.

In this case, Digital River only needs to add product tariff codes specific to that country to your SKU groups (along with any other required compliance data) to make your products eligible for export to this country.

## Defining and managing SKU groups

Prior to launch, Digital River works with you to analyze your product catalog and understand your trading patterns (i.e., what products you're selling, where you're shipping these products from, and where you're shipping them too).

We then help classify your products and determine the [compliance requirements](setting-up-sku-groups.md#product-compliance-data-in-sku-groups) for each category. That information is used to define and create your SKU groups.

Once created, you have access to each [SKU group's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) unique identifier and alias.

### The SKU group

Digital River exposes a [SKU group's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) unique identifier and alias.

#### Unique identifier

A [SKU group's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) unique `id` reflects the products that are associated with it. For example, if your site sells computer accessories, your SKU groups might have some of the following `id` values:

* `wireless-keyboards`
* `wireless-mice`
* `memory-cards`
* `docking-stations`

You use can use this identifier to (1) [associate SKU groups with products](setting-up-sku-groups.md#using-sku-groups-in-transactions) and (2) [list SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listSkuGroups).

#### Alias

A [SKU group's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) `alias` is meant to provide a more detailed description of the SKU group. For example, a SKU group with an `id` of `wireless-keyboards` might have an `alias` of `wireless keyboards with lithium-ion batteries`.

### **Managing SKU groups**

Digital River and you are responsible for:

* Defining [product compliance data](setting-up-sku-groups.md#product-compliance-data-in-sku-groups) in your [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups)
* Ensuring that the compliance data in your SKU groups remains up to date

Digital River is responsible for:

* Creating SKU groups
* Updating SKU groups
* Deleting SKU groups

You are responsible for:

* [Associating SKU groups with your products](setting-up-sku-groups.md#using-sku-groups-in-transactions)
* Dissociating SKU groups from your products
* Informing Digital River of changes to your SKU group requirements

## Associating SKU groups <a href="#using-sku-groups-in-transactions" id="using-sku-groups-in-transactions"></a>

Depending on how you decide to send product data in [create checkout](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) or [create checkout session](../integration-options/low-code-checkouts/drop-in-checkout.md#product-data) requests, you need to either (1) associate your [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) with [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) or (2) associate your SKU groups with products in your system.

{% hint style="info" %}
You can associate SKU Groups with SKUs by specifying `skuGroupId` in the body of a [`POST/skus`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createSkus), [`POST/skus/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateSkus), or [`PUT/skus/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/upsertSkus) request.
{% endhint %}

A [`GET/sku-groups`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSkuGroups) request provides a menu of your available SKU groups:

```javascript
{
    "hasMore": false,
    "data": [
        {
            "id": "wireless-keyboards",
            "alias": "Wireless keyboards with lithium-ion batteries"
        },
        {
            "id": "wireless-mice",
            "alias": "Wireless mice with lithium-ion batteries"
        },
        {
            "id": "memory-cards",
            "alias": "Compact flash memory cards"
        },
        {
            "id": "docking-stations",
            "alias": "Port replicator/hub docking stations"
        }
    ]
}
```

You could use this returned data to run a job that associates each SKU group with the appropriate SKUs in our system or products in your system. (e.g., For each of your SKUs that describe a wireless keyboard, set its `skuGroupId` to `wireless-keyboards`).

You could also use a `GET/sku-groups` to help you build a GUI widget in your admin portal that allows users to associate and disassociate SKU groups with SKUs and products.

## Migrating to SKU groups

If you’re currently using [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) and are considering a migration to [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) (or are in the process of doing so already), then you should be aware that for every `items[]` you add to a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or a [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions), SKU group data takes precedence over SKU data.

This prioritization logic applies to any differing [tax codes](creating-and-updating-skus.md#tax-code), [harmonized system codes](creating-and-updating-skus.md#harmonized-system-code), and [export control classification numbers](creating-and-updating-skus.md#eccn) that are stored in both the SKU and its associated SKU group.

For example, let’s say an `items[]` in a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) contains a reference to a SKU whose [`taxCode`](creating-and-updating-skus.md#tax-code) is     `4323.310_A` and that same SKU is associated with a SKU group which stores a different tax code.

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    "id": "7ce5a1a4-9b2b-419c-b6d0-4be836c273f9",
    ...
    "items": [
        {
            "id": "f131a7b3-c1bb-4c83-bd8a-c0ba2bcc3b0f",
            "skuId": "13e038fe-0b23-4502-86c5-ab4496a9674d",
            ...
            "tax": {
                "rate": 0.07525,
                "amount": 1.51
            },
            ...
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="SKU" %}
```javascript
{
    "id": "13e038fe-0b23-4502-86c5-ab4496a9674d",
    "createdTime": "2022-05-20T16:33:51Z",
    "name": "Widget",
    "eccn": "EAR99",
    "updatedTime": "2022-05-20T17:04:40Z",
    "taxCode": "4323.310_A",
    "countryOfOrigin": "US",
    "fulfill": false,
    "hsCode": "1006.20.4025",
    "liveMode": false,
    "physical": true,
    "skuGroupId": "ae38fd2b-2ab1-4218-9e3c-bc9881eb19f0"
}
```
{% endtab %}
{% endtabs %}

In this case, Digital River’s tax service uses the SKU group’s tax code when computing that line item's taxes. The service also uses that same tax code to determine whether the item’s products should be treated as [physical or digital goods](skus.md#how-products-are-classified-as-physical-or-digital).

&#x20;For more details, refer to:

* [Sending product data in checkouts](../integration-options/checkouts/creating-checkouts/describing-the-items/#send-basic-data-in-skus-and-compliance-data-in-sku-groups)
* [Basic versus compliance product data](skus.md#basic-versus-compliance-product-data)
* [Product compliance data in SKU groups](setting-up-sku-groups.md#product-compliance-data-in-sku-groups)
