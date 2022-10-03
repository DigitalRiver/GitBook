---
description: Understand the types of products.
---

# Product types

## Individual product

An individual product is usually a single item (such as a downloadable song from a recording artist) or many single items sold as a single product (such as a collection or box set). Use the `POST /products` request to [create an individual product](../../asynchronous-product-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) and the `POST /products/{productId}` request to [update an individual product](../../asynchronous-product-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product). There are no [product variations](product-types.md#product-variations) associated with it.

{% hint style="info" %}
If you need to [convert an individual product to a base product or a base product to an individual product](https://help.digitalriver.com/help/gc/Products/All-Products/Editing-a-product.htm#AddingRemovingVariations), you need to do it in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
{% endhint %}

## Base product

A base product contains the common attributes and settings for all variations of that product. For example, a product can come in different colors, sizes, or versions. In this instance, it would be easier and less time-consuming to maintain one base product with variations than to maintain a handful of individual products that are nearly the same. If you think your store may benefit from streamlining your catalog in this way, contact your Store Operations team.

Use the `POST /products` request to [create a base product](../../asynchronous-product-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) and the `POST /products/{productId}` request to [update a base product](../../asynchronous-product-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product).&#x20;

You can choose to either:

* [Create a base product first and add the product variations later](product-types.md#create-the-base-product-first)
* [Create the base products and product variations in one call](product-types.md#undefined)

### Create the base product first

[Create the base product](../../asynchronous-product-api/creating-or-updating-a-product.md#creating-a-base-or-individual-product) first (including supported locales, delivery types, store images, and so on). If you chose not to define some of the attributes, then those attributes will not be available when you [add a product variation](../../asynchronous-product-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product).

{% hint style="success" %}
Define as many attributes as you can in the base product before you create a product variation.
{% endhint %}

You can [add the product variations](../../asynchronous-product-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product) to that base product later.

### Create the base product and product variations

You can [create a base product and all of its product variations](../../asynchronous-product-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) using one call  by adding the [`variations` ](../../asynchronous-product-api/creating-or-updating-a-product.md#variations)object to the payload. When doing so, the base product attributes will be copied to each product variation. You can update the unique attributes for a product variation by providing the modified attributes for the product variation in the payload when you [update the product variation](../../asynchronous-product-api/adding-or-updating-a-product-variation.md#updating-a-specific-product-variation-for-a-base-product). <mark style="background-color:orange;">??? I need examples. Can you fully populate the variations object with the unique attributes for each product variation in the payload?  My the text above I wrote based off the confluence pages. I think we need more context here. ???</mark>

## Product variations

Product variations are different versions of a base product such as different operating systems versions, sizes, or capacities that a shopper can purchase from your store.

When you [add a product variation](../../asynchronous-product-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product), the system copies the attributes from the base product to the variation. For example, if two variations of a base product require the same product images, add those images to the base product before creating your variations. You need to change the appropriate attributes and settings to make that variation unique. Each product variation contains attributes and settings that are unique to that product variation.&#x20;

## Physical and digital products

Use the Product Admin API used fulfillment types (`fulfillmentTypes`) to define how products are delivered or sent to shoppers. The options are `physical` or `digital`. Digital River supports two types of digital products: subscription products and download products.
