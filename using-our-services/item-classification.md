---
description: >-
  Gain a better understanding of how the item classification service works and
  how you can use it to sell your products across international borders
---

# Item classification

Digital River's item classification service takes the information you give us about your products and then, for each country they're sold into, identifies their [tariff codes](../general-resources/glossary.md#tariff-code).&#x20;

On this page, you'll find information on:

* [How to use the item classification service in checkouts](item-classification.md#item-classification-in-checkouts)
* [How to access a product's tariff codes](item-classification.md#accessing-a-products-tariff-codes)&#x20;

## Item classification in checkouts

To trigger a call to the item classification service at checkout time, you first need to make sure your Digital River representative has enabled the [landed cost](../integration-options/checkouts/creating-checkouts/landed-costs.md) feature. Additionally, you must configure your [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [checkout-session](../developer-resources/digital-river-api-reference/checkout-sessions.md) so that:

* `shipFrom.address.country` (or `items[].shipFrom.address.country`) and `shipTo.address.country` are assigned different values.&#x20;

{% hint style="info" %}
Not all transactions that involve shipping goods from one country and into another invoke a call to item classification. In some cases, due to trade agreements that exist between nations, products in international shipments don't require tariff codes. For details, refer to [Cross border](../general-resources/glossary.md#cross-border).
{% endhint %}

* There's at least one [physical `items[]`](../product-management/skus.md#how-products-are-classified-as-physical-or-digital), each of which must have a `description`  that has a maximum length of 4000 characters, and a [`skuGroupId`](../product-management/setting-up-sku-groups.md) that's either sent in [`productDetails`](../product-management/using-product-details.md) or stored in the [SKU](../product-management/creating-and-updating-skus.md) referenced by `skuId`.&#x20;
* Each of these `items[]` must also have one or more product taxonomies. Depending on how you send us your product data, you can build these classification schemes by defining `itemBreadcrumb` or `categories`.\
  \
  For details, refer to:
  * [Item breadcrumb](../product-management/creating-and-updating-skus.md#item-breadcrumb) on [Managing SKUs](../product-management/creating-and-updating-skus.md)&#x20;
  * [Item breadcrumb and categories](../product-management/using-product-details.md#item-breadcrumb-and-categories) on [Using product details](../product-management/using-product-details.md).\

* [`shippingChoice.shippingTerms`](../general-resources/glossary.md#shipping-terms) is either omitted, undefined, or assigned a value of `DDP`.

If the goods are shipping [cross-border](../general-resources/glossary.md#cross-border) and (1) `description` and/or (2)  `itemBreadcrumb` / `categories` are missing, then a request to create or update either of these API resources returns the following error:

{% code title="400" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "missing_parameter",
            "message": "itemBreadcrumb and description required"
        }
    ]
}
```
{% endcode %}

We highly recommend that your SKUs and `productDetails` also have a `url`, `image` , and `countryOfOrigin`. Defining these parameters gives the classification service more data to work with when trying to determine a product's tariff codes.&#x20;

In general, sending detailed, high-quality data in the request increases the probability that the service returns tariff codes which match the values assigned to your products by each importation country.&#x20;

It's important that these predicted and actual tariff codes are the same. If they're not, then customers might be assessed too much or too little import taxes and duties at checkout. Incorrectly classified products can also result in non-compliance penalties, delays at the border, and even, in extreme cases, seizure of the goods or the revoking of import privileges.

## Accessing a product's tariff codes

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), each applicable `items[]` is assigned a `tariffCode` which, once the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is successfully created, gets passed to that resource as well.

{% hint style="info" %}
If you select either [low-code checkout option](../integration-options/low-code-checkouts/) , you can find the `checkoutId` in the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).&#x20;
{% endhint %}

{% tabs %}
{% tab title="Checkout" %}
```json
{
    "id": "4d690796-cb01-42e3-bc6c-1eb56f8a5386",
   ...
    "shipTo": {
        "address": {
           ...
            "country": "DE"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    ...
    "items": [
        {
            "id": "110f9716-4480-44a8-9c13-a9a447c0e95a",
            "skuId": "3feb3c3d-a584-44c9-8426-086bc9677994",
            "productDetails": {
                "id": "3feb3c3d-a584-44c9-8426-086bc9677994",
                "name": "Gungnir",
                ...
                "image": "https://en.wikipedia.org/wiki/Gungnir#/media/File:Odin-Lawrie-Highsmith.jpeg",
                "url": "https://en.wikipedia.org/wiki/Gungnir",
                "skuGroupId": "62b05273-ec28-44ab-9e55-a7a3eef99fdb",
                "description": "The mighty spear of Odin",
                "countryOfOrigin": "NO",
                "itemBreadcrumb": "Spears > Ancient > Mens > Metal"
            },
            ...
            "tariffCode": "7078638506",
            ...
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="Order" %}
```json
{
    "id": "277803930336",
   ...
    "shipTo": {
        "address": {
            ...
            "country": "DE"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    ...
    "items": [
        {
            "id": "209354060336",
            "skuId": "3feb3c3d-a584-44c9-8426-086bc9677994",
            "productDetails": {
                "id": "3feb3c3d-a584-44c9-8426-086bc9677994",
                "name": "Gungnir",
                ...
                "image": "https://en.wikipedia.org/wiki/Gungnir#/media/File:Odin-Lawrie-Highsmith.jpeg",
                "url": "https://en.wikipedia.org/wiki/Gungnir",
                "skuGroupId": "62b05273-ec28-44ab-9e55-a7a3eef99fdb",
                "weight": 431,
                "weightUnit": "kg",
                "description": "The mighty spear of Odin",
                "countryOfOrigin": "NO",
                "itemBreadcrumb": "Spears > Ancient > Mens > Metal"
            },
            ...
            "tariffCode": "7078638506",
            ...
        }
    ],
    ...
    "checkoutId": "4d690796-cb01-42e3-bc6c-1eb56f8a5386"
}
```
{% endtab %}
{% endtabs %}

The first time a product is sold into an country, it can take 24-48 hours before its successfully classified. As a result, `items[].tariffCode` might initially be assigned a default, harmonized value until its full, country-specific code is determined and added to subsequent [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

To determine the status of a product classification request, you'll need to look at `tariffRecord.tariffCodes[]` in the [SKUs resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs). Alternatively, you can get this information on the [SKU details page in the Digital River Dashboard](../administration/dashboard/catalog/skus/).&#x20;

{% hint style="info" %}
If you pass [`productDetails`](../product-management/using-product-details.md) at checkout-time, Digital River creates a [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) to represent that object.
{% endhint %}

Each element of a [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `tariffCodes[]` contains a `status`, whose possible values are `PENDING`, `CLASSIFIED`, and `CANNOT_BE_CLASSIFIED`. If `status` is `CLASSIFIED`, then the element also contains a `code` that is specific to that importation `country`.&#x20;

{% hint style="success" %}
In the following [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs), the list of `tariffCodes[]` has been shortened for demonstration purposes.
{% endhint %}

{% code title="SKU" overflow="wrap" %}
```json
{
    "id": "130015182",
    "name": "Blue Aviator - XXXL",
    ...
    "description": " T-shirts, singlets and other vests of cotton, knitted or crocheted.",
    ...
    "physical": false,
    "itemBreadcrumb": "Apparel > Knitted or crocheted > Cotton > T-shirts; Apparel > Knitted or crocheted > Cotton > Singlets; Apparel > Knitted or crocheted > Cotton > Vests",
    "tariffRecord": {
        "hsCode": "610910",
        "tariffCodes": [
            {
                "country": "AX",
                "code": "6109100090",
                "status": "CLASSIFIED"
            },
            {
                "country": "AL",
                "code": "61091000",
                "status": "CLASSIFIED"
            },
            ...
            {
                "country": "NZ",
                "code": "6109101200F",
                "status": "CLASSIFIED"
            },
            ...
            {
                "country": "MF",
                "status": "PENDING"
            },
            ...
            {
                "country": "VC",
                "code": "61091010",
                "status": "CLASSIFIED"
            },
            {
                "country": "WS",
                "code": "61091090",
                "status": "CLASSIFIED"
            },
            ...
            {
                "country": "FR",
                "code": "6109100010",
                "status": "CLASSIFIED"
            },
            {
                "country": "GF",
                "code": "6109100010",
                "status": "CLASSIFIED"
            },
            ...
        ]
    }
}
```
{% endcode %}

{% hint style="warning" %}
In the unlikely event that a `tarriffCodes[]` has a `status` of `CANNOT_BE_CLASSIFIED`, work with your Digital River representative to resolve the issue.&#x20;
{% endhint %}

Over time, as more of your products are shipped into an increasing number of countries, the service has methods to expedite the classification process and make each `items[].tariffCode` that's assigned to a [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) more precise.&#x20;

For example, even if one of your products has never been sold into an individual country, we might already know its country-specific `tariffCodes[].code`. This is because certain groups of nations, such as those in the European Union, have trade agreements in place that standardize these values among their members.&#x20;

So, to take one example, if your product sells into Germany, we might not know the full `code` assigned to it by that country. But once the classification service makes a determination and `status` moves to `CLASSIFIED`, we create a `tariffCodes[]` for each `country` participating in the EU system and assign the same `code` to each. This means that, in the future, when customers in any of these nations purchase that product, we'll already have the value we need.

Additionally, once a [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) has been assigned even just a single country-specific `code`, we can extract the first six digits of that value, which is universal among all nations, and store it in the SKU's `tariffRecord.hsCode`. That value can then be assigned to `items[].tariffCodes` in future [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) shipping to countries for which we don't yet have a full `code`.

