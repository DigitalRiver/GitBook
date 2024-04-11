---
description: Understand how to use the productDetails object
---

# Using product details

A `productDetails` object contains [basic product data](skus.md#basic-versus-compliance-product-data).&#x20;

If you decide to use `productDetails`, you'll need to retrieve product data from your system at checkout-time and then use it to define the object. Since you don't persist `productDetails` in Digital River's system, this object reduces your catalog management requirements.

If your integration currently uses [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) and you're considering a migration, you should be aware of the [common attributes in product details and SKUs](using-product-details.md#common-attributes-in-product-details-and-skus).

## Product details

You'll most commonly use `productDetails` in [create checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) and [create checkout session](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession) requests to send Digital River the following [basic product data](skus.md#basic-versus-compliance-product-data):

{% hint style="info" %}
For complete specifications, refer to the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and [Checkout Sessions API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) reference documentation.
{% endhint %}

* [Unique identifier](using-product-details.md#unique-identifier)
* [Unique SKU group identifier](using-product-details.md#unique-sku-group-identifier)
* [Country of origin](using-product-details.md#country-of-origin)
* [Name and description](using-product-details.md#name-and-description)
* [Image and url](using-product-details.md#image-and-url)
* [Weight and weight unit](using-product-details.md#weight-and-weight-unit)
* [Part number](using-product-details.md#part-number)

{% code title="POST /checkouts" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    ...
    "items": [
        {
            "productDetails": {
                "id": "2837a981-9e41-408b-a1b2-ffa3223bc505",
                "skuGroupId": "wireless-keyboards",
                "name": "Basic wireless keyboard",
                "description": "A simple, basic wireless keyboard",
                "url": "https://www.company.com/basic-wireless-keyboard",
                "countryOfOrigin": "US",
                "image": "https://www.company.com/basic-wireless-keyboard/image",
                "weight": 1,
                "weightUnit": "kg",
                "partNumber": "ce1fd95d-b211-47e8-a9b7-9941a4ce9d7a"
            },
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endcode %}

### Unique identifier

The `id` in `productDetails` should represent the unique identifier of the product in your system.

### Unique SKU group identifier

In `productDetails`, a `skuGroupId` identifies the [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) that the product belongs to. You're required to provide this identifier because Digital River uses it to access this [product's compliance data](skus.md#basic-versus-compliance-product-data).

For details, refer to [Grouping SKUs](setting-up-sku-groups.md).

In [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), if you send `productDetails` that doesn't contain a `skuGroupId`, then the following error is thrown:

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "skuGroupId",
            "message": "An item of type sku is missing a skuGroupId parameter."
        }
    ]
}
```
{% endcode %}

### Country of origin

The `countryOfOrigin` is a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard. This attribute represents the country where a product was manufactured.

In [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), if you send `productDetails`, and it doesn't contain `countryOfOrigin`, then the following error is thrown:

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "parameter": "countryOfOrigin",
            "message": "must not be null"
        }
    ]
}
```
{% endcode %}

In [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), if you send `productDetails`, and it contains an invalid `countryOfOrigin`, then the following error is thrown:

{% code title="400 Bad Request" %}
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
{% endcode %}

### Item breadcrumb and categories

In `productDetails`, you can define a parameter that represents a hierarchical classification system which organizes and categorize your products based on their attributes, characteristics, and relationships.

The parameter's name depends on the resource you're creating:

<table><thead><tr><th width="195">Resource</th><th>Parameter name</th></tr></thead><tbody><tr><td><a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts">Checkouts</a></td><td><code>itemBreadcrumb</code></td></tr><tr><td><a href="../developer-resources/digital-river-api-reference/checkout-sessions.md">Checkout-sessions</a></td><td><code>categories</code></td></tr></tbody></table>

You'll typically structure `itemBreadcrumb` / `categories` by defining a broad top-level category and, as you move down the hierarchy, getting more specific at each subsequent level.

You might have built similar data structures that inventory your products and make it easier for customers to find what they're looking for. In that case, we recommend using this same data.&#x20;

If you're engaging the [item classification service](../using-our-services/item-classification.md), then all of your [physical products](skus.md#how-products-are-classified-as-physical-or-digital) must have an `itemBreadcrumb` / `categories`.&#x20;

{% hint style="success" %}
Even if you're not currently making [cross-border](../general-resources/glossary.md#cross-border) sales, it's best practice to define this parameter so that, in the event you do start selling internationally, you're better positioned to get started.
{% endhint %}

We recommend making your taxonomies as detailed as possible. By doing so, you increase the probability that the [tariff codes](../general-resources/glossary.md#tariff-code) returned by the service are accurate.&#x20;

For example, `Clothing > Women’s Jeans` is an acceptable value but `Clothing > Women’s Clothing > Jeans > Bootcut Jeans` will likely result in more accurate classifications. You can provide multiple hierarchies, just make sure to separate each with a `;` (semi-colon).&#x20;

Although not technically required, it's highly recommended that you define `itemBreadcrumb` in English. If its value is in a different language, then the classification service will disregard this data point.

### Name and description

In `productDetails`, the `name` should represent the product's brand name and `description` should provide more details about the product.

A `name` is required but `description` is optional. If you assign a string to `description`, then we recommend that you limit its length to 1000 characters or less.&#x20;

{% hint style="success" %}
In [low-code checkouts](../integration-options/low-code-checkouts/), `name` is displayed in the order summary section.
{% endhint %}

### Image and url

In `productDetails`, you can use:

* `image` to specify the URL of a resource that contains the product's image. It should be similar to the image(s) you display to customers while they are reviewing products in your store.
* `url` to specify the address of a resource that contains the product's description.

If your integration gives customers the option to use [ApplePay](../payments/payment-integrations-1/digitalriver.js/payment-methods/apple-pay.md), [GooglePay](../payments/payment-integrations-1/digitalriver.js/payment-methods/google-pay.md), or [Klarna](../payments/payment-integrations-1/digitalriver.js/payment-methods/klarna.md) then `productDetails` must contain an `image` and `url`.

In [Prebuilt Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md), each `items[].productDetails.image` in a [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) is displayed in the [checkout modal's](../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) order summary section.&#x20;

In [Global logistics](../using-our-services/global-logistics.md), depending on your [logistics partner's](../using-our-services/global-logistics.md#global-logistics-providers) setup, both `image` and `url` are often added to the transaction's customs documentation, thereby allowing officials to obtain information about the product during the pre-clearance phase of an importation.

### Weight and weight unit

For [physical products](skus.md#how-products-are-classified-as-physical-or-digital), `productDetails` can be used to send a `weight` denoted by `weightUnit`. The enumerated `weightUnit` values are `oz`, `lb`, `g`, and `kg`.

If you provide a `weight` but not a `weightUnit`, then the value defaults to `oz`.

If your site intends on selling physical products [cross-border](../general-resources/glossary.md#cross-border), then we recommend that you pass the `weight` and `weightUnit` of all of your catalog's [physical products](skus.md#how-products-are-classified-as-physical-or-digital).

In some countries, such as Switzerland, custom officials use a product's weight when calculating import duties. As a result, without this data, Digital River is unable to calculate [landed costs](../integration-options/checkouts/creating-checkouts/landed-costs.md).

If you send a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkout request whose `shipTo.address.country` represents one of these nations, and any `productDetails` in the checkout's [`items[]`](../integration-options/checkouts/creating-checkouts/describing-the-items/) are missing `weight`, then the following error is thrown:

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

### Part number

A `productDetails` can contain a `partNumber`. It represents a unique manufacturer part number (MPN) issued by manufacturers to identify a part or product.

MPNs are meant to be static identifiers of a part/product, universal to all distributors, wholesalers, and resellers. They allow customers to accurately identify exact parts and protect themselves from counterfeits.

If two parts or products originate from two different manufacturers, then each must have its own MPN. These identifiers are especially relevant for automotive and consumer electronics, due to the numerous parts in these complex products.

## Common attributes in product details and SKUs

The attributes in [SKUs](skus.md#skus) and [`productDetails`](skus.md#product-details) are nearly identical. The key exceptions are `taxCode`, `eccn`, and `hsCode`, which exist in SKUs but not in `productDetails`.

However, since these attributes hold [compliance data](skus.md#basic-versus-compliance-product-data), they're contained in the referenced [SKU group](setting-up-sku-groups.md).

For details, refer to [Grouping SKUs](setting-up-sku-groups.md).

{% hint style="info" %}
SKUs also have a [`manufacturerId`](creating-and-updating-skus.md#manufacturer-id-and-part-number) and this attribute is not in `productDetails`.

In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), `manufacturerId` is used to set up products in warehouses. But since that process is handled prior to deployment there's no need to send `manufacturerId` at checkout-time.
{% endhint %}
