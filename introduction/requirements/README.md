---
description: Learn about the requirements for the BigCommerce app.
---

# Requirements

You must meet the following requirements before you can integrate the app.

* You must use optimized one-page checkout.
* You must have the Digital River Payments, Fraud, Tax & Compliance Management app (Digital River **** app) installed.
* You must not have any other tax provider app installed.
* You must not have any other payment provider connected.
* You must have a phone number set to required for shipping and billing information on checkout.
* You must use the [Adding Products (v3](https://support.bigcommerce.com/s/article/Adding-Products-v3?language=en\_US)) interface.
* You must use the [Product Options (v3)](https://support.bigcommerce.com/s/article/Product-Options-v3?language=en\_US) interface.

### Product setup requirements&#x20;

You must fill out the following fields for each product:

* [SKU](https://docs.digitalriver.com/digital-river-api/product-management/skus#skus)
* [Country of origin](https://docs.digitalriver.com/digital-river-api/product-management/creating-and-updating-skus#country-of-origin)&#x20;
* [Export Control Classification Number](https://docs.digitalriver.com/digital-river-api/product-management/creating-and-updating-skus#eccn) (ECCN)–You can add the ECCN added through a Custom Field. The field name must be ECCN.&#x20;
* [Tax Code](https://docs.digitalriver.com/digital-river-api/product-management/creating-and-updating-skus#tax-code)
* ``[`skuGroupId`](https://docs.digitalriver.com/digital-river-api/product-management/creating-and-updating-skus#sku-group-identifier)–The `skuGroupId` uniquely identifies a [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) configured for your Digital River account. A SKU group allows you to define the global markets, trading patterns, and their functionality. For more information, see [Grouping SKUs](https://docs.digitalriver.com/digital-river-api/product-management/setting-up-sku-groups). To configure your SKU groups, contact your Digital River Account Manager.

{% hint style="info" %}
When updating the `skuGroupId`, you must also update or change the **Basic Product** details. When the webhook triggers, this ensures the product details are synchronized with Digital River.
{% endhint %}

