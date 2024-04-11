---
description: Learn more about the standards related to products and SKUs
---

# Products and SKUs

The [checklist items](products-and-skus.md#integration-checklist) and [standards](products-and-skus.md#integration-standards) in this section cover how to manage your products in the Digital River APIs.

On this page, the [integration checklist](products-and-skus.md#integration-checklist) that you should use depends on the product data model you employ. For more information, refer to the:

* [Defining goods and services page](../../../product-management/skus.md)
* [Sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items](../../../integration-options/checkouts/creating-checkouts/describing-the-items/) page

## Integration checklists <a href="#integration-checklist" id="integration-checklist"></a>

In this section, the integration checklist that you should work from depends on the [product data model](../../../product-management/skus.md) you employ.

{% hint style="info" %}
For more information refer to the [sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items](../../../integration-options/checkouts/creating-checkouts/describing-the-items/) page.
{% endhint %}

Click any checklist item to be provided more details on how to meet the integration standard.

### SKUs only checklist

* [ ] [Do you have a method for manually synchronizing a full product catalog using the SKUs API?](products-and-skus.md#manually-synchronize-your-catalog)
* [ ] [Do you have a scheduled job or real-time trigger to synchronize new and updated products in your catalog with their corresponding SKUs in our system?](products-and-skus.md#automatically-synchronize-your-catalog)
* [ ] [Can you capture a product's tax code, ECCN, and country of origin within your product admin interface?](products-and-skus.md#capture-sku-attributes)
* [ ] [Does your integration use your source system's unique product identifier as the SKU identifier when interfacing with the SKUs API?](products-and-skus.md#ensure-product-and-sku-identifiers-match)

### SKUs with SKU groups checklist

* [ ] [Do you have a method for manually synchronizing a full product catalog using the SKUs API?](products-and-skus.md#manually-synchronize-your-catalog)
* [ ] [Do you have a scheduled job or real-time trigger to synchronize new and updated products in your catalog with their corresponding SKUs in our system?](products-and-skus.md#automatically-synchronize-your-catalog)
* [ ] [Does your integration use your source system's unique product identifier (UUID) as the SKU identifier when interfacing with the SKUs API?](products-and-skus.md#ensure-product-and-sku-identifiers-match)
* [ ] [Have you associated a SKU group with each of your SKU's?](products-and-skus.md#associate-a-sku-group-with-each-sku)

### Product details with SKU groups checklist

* [ ] [Have you associated a SKU group with each of the product's in your system?](products-and-skus.md#associate-a-sku-group-with-each-product-in-your-system)

## Integration standards

The product and SKU standards that apply to your integration are dependent on which of the above :point\_up: checklists you're using.

### Manually synchronize your catalog

You should have a tool that manually imports and then allows you to periodically update your products in Digital River's system through the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs). Your platform's admin interface most likely has a product management page already in place. You can simply modify this page to perform [SKU imports and updates](../../../product-management/creating-and-updating-skus.md#creating-and-updating-a-sku).

### Automatically synchronize your catalog

Product catalogs are often very large. So, to optimize performance, you should synch your products and [SKUs](../../../product-management/skus.md) on a timed schedule or by using some similar trigger.

These scheduled jobs should make as few calls to the [SKUs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) as possible. Therefore, we suggest you use a delta to only update the attributes in a SKU that changed in its corresponding product. This prevents you from having to overwrite every SKU value each time you run a synchronization job.

### Capture SKU attributes

If you're [sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) by referencing SKUs that don't belong to [SKU groups](../../../product-management/setting-up-sku-groups.md), then you should add the following attributes to the product schema in your commerce platform:

* [Export Control Classification Number](../../../product-management/creating-and-updating-skus.md#eccn)
* [Country of origin](../../../product-management/creating-and-updating-skus.md#country-of-origin)
* [Tax code](../../../product-management/creating-and-updating-skus.md#tax-code)

Similarly, regardless of whether or not you associate SKU groups with SKUs, if you're [sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) by referencing SKUs, you should also add the following attributes to your platform's product schema:

* [Part number](../../../product-management/creating-and-updating-skus.md#manufacturer-id-and-part-number)
* [Weight and weight unit](../../../product-management/creating-and-updating-skus.md#weight-and-weight-unit)
* [Image and URL](../../../product-management/creating-and-updating-skus.md#image-and-url)
* [Fulfillment coordinator](../../../product-management/creating-and-updating-skus.md#managed-fulfillments)

When you set these values in your admin interface, you can then [sync your products with their corresponding SKU's](products-and-skus.md#automatically-synchronize-your-catalog) in Digital River's system.

### Ensure product and SKU identifiers match

The identifier of your product should match the [identifier of its corresponding SKU](../../../product-management/creating-and-updating-skus.md#unique-identifier) in our system. Its important that these values are the same. This ensures that synchronization is possible and that the SKUs work properly during [checkouts](../../../integration-options/checkouts/creating-checkouts/).

### Associate a SKU group with each SKU

Prior to deployment, you should [associate a SKU group with each of your SKU's in our system](../../../product-management/setting-up-sku-groups.md#using-sku-groups-in-transactions).

### Associate a SKU group with each product in your system

Prior to deployment, you should [associate a SKU group with each product in your system](../../../product-management/setting-up-sku-groups.md#using-sku-groups-in-transactions).

## API interfaces

| Documentation                                                                                                                                                                                                                                                           | Direct API                                                                      | PHP SDK                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [Defining goods and services](../../../product-management/skus.md), [Grouping SKUs](../../../product-management/setting-up-sku-groups.md), [Sending product data](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) | [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) | [SKUs](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Sku.md) |
