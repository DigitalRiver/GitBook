---
description: >-
  Gain a better understanding of selling entities and how to use them in your
  integration
---

# Selling entities

As the [authorized reseller](../../../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor) of your products and services, Digital River engages with [multiple local selling entities](selling-entities.md#supported-selling-entities).

These entities play a role in determining a transaction's eligible [payment methods](../../../payments/supported-payment-methods/), payment processors, and fulfillment models. In addition, we use them when computing taxes and deciding whether [tax identifiers](tax-identifiers.md) and [tax certificates](../../../customer-management/setting-tax-related-attributes.md#tax-certificates) can be applied to purchases.

A `sellingEntity` gets dynamically assigned during the [checkout process](./):

{% tabs %}
{% tab title="Checkout" %}
```javascript
{
    ...
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    ...
}
```
{% endtab %}
{% endtabs %}

How Digital River selects a `sellingEntity` depends on whether the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`items[]`](describing-the-items/) are [physical or digital](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital). If `items[]` contains physical goods, we compare the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shipFrom.address.country` to its `shipTo.address.country`. Otherwise, we look at `billTo.address.country`.

In addition, we analyze your eligible entities, which are determined by your trading patterns and your contract with Digital River.

{% hint style="success" %}
Specific eligible entities can be enabled in your contract depending on your needs.
{% endhint %}

You can [use selling entities](selling-entities.md#using-selling-entities) to configure front-end methods that display required disclosures and validate customer-submitted data.

## Supported selling entities

The Digital River APIs support the following selling entities:

* Digital River, Inc.
* DR globalTech, Inc.
* Digital River Ireland Ltd.
* Digital River UK
* DR Japan
* Digital River Taiwan
* DR Korea

## Using selling entities

Once Digital River has enough data points to make a determination, we populate the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sellingEntity`.&#x20;

{% tabs %}
{% tab title="Checkout" %}
```json
{
    "id": "d794759b-85df-424d-b6ac-9133e09ea3da",
    ...
    "shipFrom": {
        "address": {
            ...
            "country": "TW"
        }
    },
    ...
    "sellingEntity": {},
    ...
}
```
{% endtab %}

{% tab title="Updated checkout" %}
```json
{
    "id": "d794759b-85df-424d-b6ac-9133e09ea3da",
    ...
    "shipTo": {
        "address": {
            ...
            "country": "TW"
        },
        ...
    },
    "shipFrom": {
        "address": {
            ...
            "country": "TW"
        }
    },
    ...
    "sellingEntity": {
        "id": "DR_TAIWAN-ENTITY",
        "name": "Digital River Taiwan"
    },
    ...
}
```
{% endtab %}
{% endtabs %}

You can use `sellingEntity.id` to:

* Create a [compliance element](../../../developer-resources/reference/elements/compliance-elements.md) to display Digital River's required disclosures.
* Configure the [get compliance details method](../../../developer-resources/reference/digitalriver-object.md#digitalriver.compliance.getdetails-businessentitycode-locale), which returns individual disclosures that can be displayed on your front-end.
* Create a [tax identifier element](../../../developer-resources/reference/elements/tax-identifier-element.md) to validate the format of tax identification numbers entered by customers.

## Multiple selling entity scenarios

A transaction can only be assigned a single selling entity. This means that if you submit a [`POST /checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [`POST /checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) that results in a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) with multiple [`items[]`](describing-the-items/) that can't be handled by a single selling entity, then a `400 Bad Request` with a `code` of `selling_entity_not_found` is returned.
