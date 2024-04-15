---
description: >-
  Gain a better understanding of a SKU's attributes and how they affect
  downstream processes
---

# Managing SKUs

On this page, you'll find information on a [SKUs](skus.md#skus) key attributes.&#x20;

{% hint style="info" %}
Depending on how you send product data in [create checkout](../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) or [create checkout-session](../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) requests, your [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) might contain [compliance and/or basic product data](skus.md#basic-versus-compliance-product-data).
{% endhint %}

Once you define a [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) attributes, you can perform a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/createSkus) or [upsert](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/upsertSkus) operation. After that, the resource can be [updated](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/updateSkus) or [deleted](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/deleteSkus). You can also [retrieve a SKU by its unique identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSkus) or [search for SKUs using various query parameters](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listSkus).

## Physical or digital <a href="#how-products-are-specified-as-physical-or-digital" id="how-products-are-specified-as-physical-or-digital"></a>

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `physical` attribute indicates whether Digital River has classified the product as physical or digital.&#x20;

If `physical` is `true`, then the SKU's [`taxCode`](creating-and-updating-skus.md#tax-code) or the tax code of the SKU's [SKU group](creating-and-updating-skus.md#sku-group-identifier) represents a physical product, and vice versa.

For details, refer to [how products are classified as physical or digital](skus.md#how-products-are-classified-as-physical-or-digital) on the [Product basics](skus.md) page.

## Unique identifier

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) unique identifier is represented by `id`.

A product's identifier in your system should ideally match the SKU's `id` in ours. This ensures that synchronization is possible and that SKUs work properly throughout an [order's lifecycle](../order-management/orders/the-order-lifecycle.md). Therefore, we recommend that you specify your own `id` and ensure it matches your product's universally unique identifier.

If you don't specify `id` in the body of a [create SKU request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/createSkus), then Digital River generates and returns a unique value.

In [create](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/createSkus) and [upsert](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/upsertSkus) SKU requests, `id` must adhere to the following character set:

* Digits from `0` to `9`
* Upper case letters from `A` to `Z`
* Lower case letters from `a` to `z`
* Dots/points: `.`
* Hyphens: `-`
* Underscores: `_`

If `id` contains any other character, then a `400 Bad Request` is returned:

```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "id",
            "message": "'89&56' is not a valid SKU ID."
        }
    ]
}
```

## Item breadcrumb

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `itemBreadcrumb` represents a hierarchical classification system that organizes and categorizes your products based on their attributes, characteristics, and relationships. You'll typically structure `itemBreadcrumb` by defining a broad top-level category and, as you move down the hierarchy, getting more specific at each subsequent level.

You might have built similar data structures that inventory your products and make it easier for customers to find what they're looking for. In that case, we recommend using this same data.

If you're engaging the [item classification service](../using-our-services/item-classification.md), then all of your [physical SKUs](skus.md#how-products-are-classified-as-physical-or-digital) must have an `itemBreadcrumb`.&#x20;

{% hint style="success" %}
Even if you're not currently making [cross-border](../general-resources/glossary.md#cross-border) sales, it's best practice to define this parameter so that, in the event you do start selling internationally, you're better positioned to get started.
{% endhint %}

We recommend making your taxonomies as detailed as possible. By doing so, you increase the probability that the [tariff codes](../general-resources/glossary.md#tariff-code) returned by this service are accurate.&#x20;

For example, `Clothing > Women’s Jeans` is an acceptable value but `Clothing > Women’s Clothing > Jeans > Bootcut Jeans` will likely result in more accurate classifications. You can also define multiple hierarchies, just make sure to separate each with a `;` (semi-colon).&#x20;

Although not technically required, it's highly recommended that you define `itemBreadcrumb` in English. If its value is in a different language, then the classification service will disregard this data point. &#x20;

## Country of origin

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `countryOfOrigin` is a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard. It represents the country where a product was manufactured.

If a SKU does not have a [`skuGroupId`](creating-and-updating-skus.md#sku-group-identifier), then it must contain a `countryOfOrigin`.&#x20;

If you submit an invalid country code, then Digital River returns a  `400 Bad Request`:

```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "countryOfOrigin",
            "message": "'KP' is not a valid Country of Origin."
        }
    ]
}
```

## ECCN

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `eccn` represents its [Export Control Classification Number](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn) (ECCN).&#x20;

If a SKU does not have a [`skuGroupId`](creating-and-updating-skus.md#sku-group-identifier), then it must contain an `eccn`.

This value determines whether a product:

* Requires a U.S. export/re-export license
* Contains any other license requirements/restrictions
* Has an end use which is prohibited by applicable export control laws

Digital River's [legal documentation](https://www.digitalriver.com/legal-information/) lists [ECCNs approved](https://www.digitalriver.com/legal-other/approved-eccns/) for use in the Digital River APIs. In the table's description field, you may find additional requirements and restrictions that further limit the use of the ECCN.

{% hint style="danger" %}
Digital River can only resell products with these listed ECCNs. If you have a product with an ECCN that you'd like to be considered for addition to the list, please contact [Legal-compliance@digitalriver.com](mailto:Legal-compliance@digitalriver.com)
{% endhint %}

## Harmonized system code

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `hsCode` represents a [Harmonized System code](https://www.trade.gov/harmonized-system-hs-codes). &#x20;

The format of the code is `####.##.####`, where `#` represents a numeric digit between 0 and 9. The first six digits are mandatory. Any code longer than six digits but less than ten digits is optional and based on the country's preference. The period is not included in the character count.

Digital River validates a Harmonized System code's format. We don't however determine whether `hsCode` accurately classifies your product.

For example, the full ten-digit code for Jasmine rice in the United States is 1006.20.4025. If that's the value you specify, then we don't check to make sure your product belongs in that category.

If you submit an incorrectly formatted `hsCode`, then Digital River returns a `400 Bad Request`:

{% tabs %}
{% tab title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "hsCode",
            "message": "'1234.56.YW' is not a valid HS code."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## SKU group identifier

The `skuGroupId` uniquely identifies the [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) associated with the [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs). For details, refer to [Grouping SKUs](setting-up-sku-groups.md).

## Manufacturer id and part number

A [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `manufacturerId` and `partNumber` are only applicable to [physical products](skus.md#how-products-are-classified-as-physical-or-digital).

The `manufacturerId` represents the unique identifier of a part/product's manufacturer.

A manufacturer part number (MPN) is a unique code issued by manufacturers to identify a part/product. This is represented by a SKU's `partNumber`.

MPNs are meant to be static identifiers of a part/product, universal to all distributors, wholesalers, and resellers. They allow customers to accurately identify exact parts and protect themselves from counterfeits.

If two parts/products originate from two different manufacturers, then each must have its own MPN. These identifiers are especially relevant for automotive and consumer electronics, due to the numerous parts in these complex products.

## Managed fulfillments

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/) that use the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), you'll need to meet our [managed fulfillment requirements](creating-and-updating-skus.md#managed-fulfillment-requirements) before you can [create and update SKU-inventory item pairs](creating-and-updating-skus.md#creating-and-updating-sku-inventory-item-pairs).

#### Managed fulfillment requirements

All the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [physical SKUs](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) must meet the following requirements:

| SKU attribute        | Requirement                                                                                                                                           | Sample error                                                                                                                                                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `managedFulfillment` | The specified value must be `DRGlobalFulfillment`.                                                                                                    | <p><code>400 Bad Request</code></p><p><code>{ "type": "bad_request",</code></p><p><code>"errors": [ {</code></p><p><code>"code": "invalid_parameter", "parameter":"managedFulfillment", "message": "'DRGlobalFulfillment^&#x26;%^' is not a valid item type." }</code></p><p><code>] }</code></p>                                    |
| `taxCode`            | The specified value must be associated with a [physical product](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital).    | <p><code>400 Bad Request</code></p><p><code>{ "type": "bad_request",</code></p><p><code>"errors": [ {</code></p><p><code>"code": "invalid_parameter", "parameter": "taxCode",</code></p><p><code>"message": "'4512.100' is not a valid parameter." }</code></p><p><code>] }</code></p>                                               |
| `partNumber`         | The value must be specified.                                                                                                                          | <p><code>400 Bad Request</code></p><p><code>{ "type": "bad_request",</code></p><p><code>"errors": [ {</code></p><p><code>"code": "invalid_parameter", "parameter": "partNumber", "message": "'null' is not a valid parameter." }</code></p><p><code>] }</code></p>                                                                   |
| `manufacturerId`     | If you specify this value, then the `partNumber` must be valid. In other words, the combination of `manufacturerId` and `partNumber` must be correct. | <p><code>409 Conflict</code></p><p><code>{ "type": "conflict",</code></p><p><code>"errors": [ {</code></p><p><code>"code": "invalid_parameter", "parameter": "manufacturerId", "message": "Invalid manufacturer ID. The manufacturer ID and manufacturer part # combination could not be found." }</code></p><p><code>] }</code></p> |

#### Creating and updating SKU-Inventory Item pairs

When you [create](creating-and-updating-skus.md#creating-and-updating-a-sku) or [upsert](creating-and-updating-skus.md#upserting-a-sku) a SKU that meets our [managed fulfillment requirements](creating-and-updating-skus.md#managed-fulfillment-requirements), Digital River synchronously creates an associated [inventory item](skus.md#inventory-items). These [SKU-inventory item pairs](common-attributes.md) have [shared attributes](common-attributes.md#shared-attributes) with identical values.

{% tabs %}
{% tab title="POST /skus" %}
#### Request

```
curl --location --request POST 'https://api.digitalriver.com/skus' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "id": "sku_demo_1617140947939",
    "eccn": "EAR99",
    "countryOfOrigin": "DE",
    "taxCode": "4323.310_A",
    "partNumber": "DEMOPARTNUMBER2",
    "name": "name_demo_1617140947939",
    "weight": 8.88,
    "weightUnit": "oz",
    "metadata": {
        "application": "iOS-LLL"
    },
    "managedFulfillment": "DRGlobalFulfillment"
}'
```

#### Response

```javascript
{
    "id": "sku_demo_1617146803587",
    "createdTime": "2021-03-30T23:26:43Z",
    "name": "name_demo_1617146803587",
    "eccn": "EAR99",
    "partNumber": "DEMOPARTNUMBER2",
    "taxCode": "4323.310_A",
    "countryOfOrigin": "DE",
    "metadata": {
        "application": "iOS-LLL"
    },
    "weight": 8.88,
    "weightUnit": "oz",
    "fulfill": false,
    "allowOversell": true,
    "liveMode": false,
    "managedFulfillment": "DRGlobalFulfillment",
    "physical": true
}
```
{% endtab %}

{% tab title="GET /inventory-items/{id}" %}
#### Request

```
curl --location --request GET 'https://api.digitalriver.com/inventory-items/sku_demo_1617146803587' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw ''
```

#### Response

```javascript
{
    "id": "sku_demo_1617146803587",
    "manufacturerId": "20013",
    "partNumber": "DEMOPARTNUMBER2",
    "allowOversell": true,
    "createdTime": "2021-03-30T23:26:43Z",
    "eccn": "EAR99",
    "countryOfOrigin": "DE",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

Since the SKU's `id` and the inventory item's `id` are the same, you can use this value to [describe items in checkouts](../integration-options/checkouts/creating-checkouts/describing-the-items/), [check inventory levels](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/checking-inventory-levels.md), [request shipping quotes](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/using-shipping-quotes.md) and [make reservations](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/reserving-inventory-items.md).

Every subsequent modification of a `managedFulfillment` SKU (assuming the [update request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/updateSkus) satisfies our [managed fulfillment requirements](creating-and-updating-skus.md#managed-fulfillment-requirements)) synchronously updates the paired inventory item.

{% tabs %}
{% tab title="POST /skus/{id}" %}
#### Request

```
curl --location --request POST 'https://api.digitalriver.com/skus/sku_demo2_1617153759250' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "countryOfOrigin": "US"
}'
```

#### Response

```javascript
{
    "id": "sku_demo2_1617153759250",
    "createdTime": "2021-03-31T01:22:39Z",
    "name": "name_demo2_1617153759250",
    "eccn": "EAR99",
    "partNumber": "DEMOPARTNUMBER2",
    "updatedTime": "2021-03-31T01:23:04Z",
    "taxCode": "4323.310_A",
    "countryOfOrigin": "US",
    "metadata": {
        "application": "iOS-LLL"
    },
    "weight": 8.88,
    "weightUnit": "oz",
    "fulfill": false,
    "allowOversell": true,
    "liveMode": false,
    "managedFulfillment": "DRGlobalFulfillment",
    "physical": true
}
```
{% endtab %}

{% tab title="GET /inventory-items/{id}" %}
#### Request

```
curl --location --request GET 'https://api.digitalriver.com/inventory-items/sku_demo2_1617153759250' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw ''
```

#### Response

```javascript
{
    "id": "sku_demo2_1617153759250",
    "manufacturerId": "20013",
    "partNumber": "DEMOPARTNUMBER2",
    "allowOversell": true,
    "createdTime": "2021-03-31T01:22:43Z",
    "updatedTime": "2021-03-31T01:23:04Z",
    "eccn": "EAR99",
    "countryOfOrigin": "US",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Once Digital River creates an [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items), do not directly update or delete it through the [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items). These operations modify and delete the inventory item but do not affect its paired SKU.
{% endhint %}

When you want to remove Digital River as a product's fulfillment coordinator, set `managedFulfillment` to `null` in an [update SKU request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/updateSkus). This deletes the inventory item paired with the SKU. If you then attempt to retrieve the inventory item, you receive a `404 Not Found`.

{% tabs %}
{% tab title="POST /skus/{id}" %}
#### Request

```
curl --location --request POST 'https://api.digitalriver.com/skus/sku_demo_1617153057380' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "managedFulfillment": null
}'
```

#### Response

```javascript
{
    "id": "sku_demo_1617153057380",
    "createdTime": "2021-03-31T01:10:57Z",
    "name": "name_demo_1617153057380",
    "eccn": "EAR99",
    "partNumber": "DEMOPARTNUMBER2",
    "updatedTime": "2021-03-31T01:19:14Z",
    "taxCode": "4323.310_A",
    "countryOfOrigin": "DE",
    "metadata": {
        "application": "iOS-LLL"
    },
    "weight": 8.88,
    "weightUnit": "oz",
    "fulfill": false,
    "allowOversell": true,
    "liveMode": false,
    "physical": true
}
```
{% endtab %}

{% tab title="GET /inventory-items/{id}" %}
#### Request

```
curl --location --request GET 'https://api.digitalriver.com/inventory-items/sku_demo_1617153057380' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw ''
```

#### Response

```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "not_found",
            "parameter": "id",
            "message": "InventoryItem 'sku_demo_1617153057380' not found."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

#### Deleting SKU-Inventory Item pairs

A [delete SKU request](creating-and-updating-skus.md#deleting-a-sku) deletes both the SKU and the inventory item it's paired with.

## Name and description

A [SKU's](../administration/dashboard/catalog/skus/) `name` should represent the product's brand name and `description` should provide more details about the product.

A `name` is required but`description` is optional. If you assign a string to `description`, then we recommend that you limit its length to 1000 characters or less.&#x20;

{% hint style="success" %}
In [low-code checkouts](../integration-options/low-code-checkouts/), `name` is displayed in the order summary section.
{% endhint %}

## Image and url

You can use a [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs):

* `image` to specify the URL of a resource that holds the product's image. This resource should be similar to the image(s) you display to customers while they are reviewing products in your store.
* &#x20;`url` to specify the address of a resource that contains the product's description.

If your integration gives customers the option to use [ApplePay](../payments/payment-integrations-1/digitalriver.js/payment-methods/apple-pay.md), [GooglePay](../payments/payment-integrations-1/digitalriver.js/payment-methods/google-pay.md), or [Klarna](../payments/payment-integrations-1/digitalriver.js/payment-methods/klarna.md) then each of your SKUs must contain an `image` and `url`.

In [Prebuilt Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md), the `image` of each SKU referenced in the [checkout-sessions'](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `items[]` is displayed in the order summary section of the [checkout modal](../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window).

In [Global logistics](../using-our-services/global-logistics.md), depending on your [logistics partner's](../using-our-services/global-logistics.md#global-logistics-providers) setup, both `image` and `url` are often added to the transaction's customs documentation, thereby allowing officials to obtain information about the product during the pre-clearance phase of an importation.

## Weight and weight unit

For [physical SKUs](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), you should provide a product’s `weight` denoted in a `weightUnit`. The enumerated `weightUnit` values are `oz`, `lb`, `g`, and `kg`. If you provide `weight` but not a `weightUnit`, then the value defaults to `oz`.

If your site intends on selling physical products [cross-border](../general-resources/glossary.md#cross-border), then we recommend that you pass the `weight` and `weightUnit` of all of your catalog's [physical SKUs](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital).

In some countries, such as Switzerland, custom officials use a product's weight when calculating import duties. As a result, without this data, Digital River is unable to calculate [landed costs](../integration-options/checkouts/creating-checkouts/landed-costs.md).

If you send a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkout request whose `shipTo.address.country` represents one of these nations, and any [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) referenced in the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`items[]`](../integration-options/checkouts/creating-checkouts/describing-the-items/) is missing `weight`, then the following error is thrown:

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "message": "The weight is missing.",
            "parameter": "weight"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Allow oversell

In [Digital River coordinated fulfillments](../order-management/fulfillments.md#digital-river-coordinated-fulfillments), you may decide to build your integration such that customers can reserve out of stock items or pre-order items not yet in stock. To do this, you can use the SKU's `allowOversell` flag.

{% hint style="warning" %}
In [version](../general-resources/versioning.md) `2021-12-13` and later, you can't set a [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `allowOversell`.
{% endhint %}

If you set the flag to `true`, customers can [reserve the item](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/reserving-inventory-items.md) even when inventory is not available. When set to `false`, customers won't be able to place a hold on an item when its inventory levels are not sufficient.

## Tax code

A [SKU's](../administration/dashboard/catalog/skus/) `taxCode` determines whether Digital River classifies a product as [physical or digital](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) and ensures that taxes on it are properly assessed.&#x20;

If a SKU does not have a [`skuGroupId`](creating-and-updating-skus.md#sku-group-identifier), then it must contain a `taxCode`.

You can modify a SKU's `taxCode` in either an [upsert](creating-and-updating-skus.md#upsert-request) or [update](creating-and-updating-skus.md#creating-and-updating-a-sku) SKU request.

#### Supported tax codes

The following table lists the `taxCode` values supported by Digital River, provides a short description of each, and indicates whether it represents a [physical or digital product](creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital).

{% hint style="info" %}
If you'd like to sell a product that isn't described by any of these `taxCode`(s) , contact your account representative.
{% endhint %}

{% file src="../.gitbook/assets/Supported tax codes (1).pdf" %}
