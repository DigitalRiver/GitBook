---
description: >-
  Understand landed cost and learn how to use Digital River's landed cost
  feature
---

# Landed cost

During checkouts, [Digital River's landed cost feature](landed-costs.md#digital-rivers-landed-cost-feature) allows you to present customers with a transaction's [landed cost](landed-costs.md#what-is-landed-cost).

Once you [set up the landed cost feature](landed-costs.md#pre-deployment-configurations), it's triggered when the [necessary preconditions](landed-costs.md#triggering-the-landed-cost-feature) are met. After the feature is activated, Digital River's [landed cost service generates a calculation](landed-costs.md#how-landed-costs-are-calculated) and we return that [landed cost calculation in checkouts](landed-costs.md#how-landed-cost-is-represented) so you can display it to customers.

## What is landed cost?

Landed cost represents the total amount your customer must pay to purchase a product from one country and have it shipped to another country. Landed cost consists of:

* The value of goods in a customer's cart
* Shipping costs
* Import duties
* Taxes

## Landed cost payment options

Customers have two options to pay a transaction's full [landed cost](landed-costs.md#what-is-landed-cost):&#x20;

{% hint style="info" %}
For more information, refer to the [shipping terms](shipping-choice.md#shipping-terms) section on the [Handling shipping choice](shipping-choice.md) page.
{% endhint %}

### **Delivered duty paid (DDP)**

In this option, customers pay the full [landed cost](landed-costs.md#what-is-landed-cost) during the [checkout process](./).

### **Delivered at place (DAP)**

In this option, customers do _not_ pay the full [landed cost](landed-costs.md#what-is-landed-cost) during the [checkout process](./). Instead, they pay product and shipping costs during checkouts, and then, upon an order's delivery, they're responsible for paying duties, fees, and import taxes.

## Digital River’s landed cost feature <a href="#digital-rivers-landed-cost-feature" id="digital-rivers-landed-cost-feature"></a>

Digital River offers both a [standard](landed-costs.md#standard-landed-cost-feature) and a [guaranteed](landed-costs.md#guaranteed-landed-cost-feature) landed cost feature.

### Standard landed cost feature

You can use Digital River's standard [landed cost](landed-costs.md#what-is-landed-cost) feature to provide your customers with a landed cost estimate. However, if the estimate returned by our [landed cost service](landed-costs.md#how-landed-costs-are-calculated) is less than the actual importation costs assessed by a country's custom agency, then you're ultimately responsible for the difference.

With this feature, once an order is submitted, your fulfillment logistics provider typically relays an order's details to a shipper, who completes the customs paperwork, ships the package to the destination country, and pays the duties, fees and import taxes on behalf of your customer. The shipper then invoices you for these costs.

### Guaranteed landed cost feature

Digital River's guaranteed landed cost feature provides a guarantee to both you and the customer. You must be using the [Global Logistics solution](../../../using-our-services/global-logistics.md) to take advantage of this feature.

For more information, refer to the [guaranteed landed cost](../../../using-our-services/global-logistics.md#guaranteed-landed-cost) section on the [Global Logistics](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/integration-options/checkouts/creating-checkouts/broken-reference/README.md) page.

## Pre-deployment configurations

How you handle the pre-deployment process depends on whether you're:

* [Setting up the standard landed cost feature](landed-costs.md#setting-up-the-standard-landed-cost-feature) or
* [Setting up the guaranteed landed cost feature](landed-costs.md#setting-up-the-guaranteed-landed-cost-feature)

### Setting up the standard landed cost feature

The standard [landed cost](landed-costs.md#what-is-landed-cost) feature is available to anyone who integrates with the Digital River APIs. It's not dependent on the version you're using, how you [send product data in checkouts](describing-the-items/#sending-product-data), or who acts as your [fulfillment coordinator](../../../order-management/fulfillments.md).

Prior to using this feature, you need to complete the following steps:

**Step one**: Verify your fulfiller ships products outside of their country (not all fulfillers provide this service).

**Step two**: Determine whether your shipper is willing and able to prepay landed cost on behalf of the customer and invoice you for these costs.

**Step three**: Define your [cross-border](../../../general-resources/glossary.md#cross-border) patterns (in other words, where your products ship from and where they ship to).

{% hint style="danger" %}
The ship-to countries must be supported by Digital River and cannot include embargoed nations. For more information, refer to our [Country Guide](https://www.digitalriver.com/country-guide/).
{% endhint %}

**Step four**: Provide samples of completed customs forms, such as commercial invoices, to Digital River's compliance team for approval.

**Step five**: Sign an addendum in your Digital River contract to enable the landed cost feature (unless already specified in the order form).

**Step six**: Associate a [Harmonized System (HS) code](https://www.trade.gov/harmonized-system-hs-codes) with each of your [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital). To do this, you can (1) set [`hsCode`](../../../product-management/creating-and-updating-skus.md#harmonized-system-code) on the [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) (2) associate a [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) with the [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) or (3) reference a [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) in [`productDetails`](../../../product-management/using-product-details.md).

{% hint style="info" %}
For more information, refer to:

* [Sending product data in checkouts](describing-the-items/#sending-product-data) on the [Describing line items](describing-the-items/#sending-product-data) page
* The [Grouping SKUs](../../../product-management/setting-up-sku-groups.md) page
{% endhint %}

In this step, we recommend that you select either option two or three. These options allow you to:

* Simplify the process of assigning and managing your products' HS codes.
* Use country-specific HS tariff codes that are tailored to each transaction, thereby improving the accuracy of the [landed cost calculation](landed-costs.md#how-landed-costs-are-calculated).

### Setting up the guaranteed landed cost feature

To get a [guaranteed landed cost](landed-costs.md#guaranteed-landed-cost-feature), you must be using Digital River's [Global Logistics](../../../using-our-services/global-logistics.md) solution. For more information on how to access and set up this solution, refer to the [pre-deployment](../../../using-our-services/global-logistics.md#pre-deployment) section on the [Global Logistics](../../../using-our-services/global-logistics.md) page.

## Triggering the landed cost feature <a href="#triggering-the-landed-cost-feature" id="triggering-the-landed-cost-feature"></a>

Once you perform the [pre-deployment configurations](landed-costs.md#pre-deployment-configurations), landed cost is calculated during the [checkout process](./). To successfully [receive a landed cost calculation](landed-costs.md#how-landed-cost-is-represented) at run-time, the following preconditions must exist:

* The [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) contains [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital)
* The checkout's [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) are associated with a [Harmonized System code](https://www.trade.gov/harmonized-system-hs-codes).
* The checkout's [`taxInclusive`](configuring-taxes.md) flag must be `false`.
* The checkout contains a [`shippingChoice.amount`](shipping-choice.md#shipping-amount) and its value is inclusive of any [applied discounts](applying-a-discount.md)
* The checkout's [`shippingChoice.shippingTerms`](shipping-choice.md#shipping-terms) must be [`DDP`](shipping-choice.md#delivered-duty-paid-ddp).
* The checkout's [`shipTo.address.country`](providing-address-information.md#ship-to-address) is on the approved list
* The checkout's [`shipFrom.address.country`](providing-address-information.md#ship-from-address) and `shipTo.address.country` are specified and the values are different. Since shipments between EU countries are exempt from duties, a checkout's ship from country and ship to country can't _both_ be EU nations.

## How landed cost is calculated <a href="#how-landed-costs-are-calculated" id="how-landed-costs-are-calculated"></a>

To calculate [landed cost](landed-costs.md#what-is-landed-cost) in [applicable checkouts](landed-costs.md#triggering-the-landed-cost-feature), Digital River sends an API request to a third-party service. Based on the data provided in the request, this service calculates taxes, duties, fees, and import taxes.

We use the values returned by this service to build a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `totalAmount`. When you [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), this is what the customer is ultimately charged

#### Calculation failures

If a customer attempts to ship a product to an embargoed country, then the checkout fails:

{% tabs %}
{% tab title="409 Conflict" %}
```
{
    "type": "conflict",
    "errors": [
        {
            "code": "country_unsupported",
            "parameter": "country",
            "message": "Country 'KP' is not supported."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

Additionally, on rare occasions, the third-party landed cost service may be unavailable or unable to generate a calculation. In these cases, no [landed cost values](landed-costs.md#how-landed-cost-is-represented) are returned in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

## How landed cost is represented in checkouts <a href="#how-landed-cost-is-represented" id="how-landed-cost-is-represented"></a>

{% hint style="warning" %}
In versions `2020-09-30` and earlier, landed cost is represented by `totalDuty` and `importerOfRecordTax`.
{% endhint %}

In [checkouts that trigger the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature), we provide you an itemized breakdown of taxes, duties, fees, and import taxes. Since your customers ultimately pay these costs, you should display them during the [checkout process](./).

The [full landed cost](landed-costs.md#what-is-landed-cost) is contained in numerous attributes at both the [checkout level](landed-costs.md#order-level-attributes) and the [line item level](landed-costs.md#item-level-attributes). You can use this data to determine import duties and distinguish between taxes Digital River remits and those remitted by the shipper.

### Checkout level attributes <a href="#order-level-attributes" id="order-level-attributes"></a>

A [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `totalAmount` is ultimately what the customer is charged when you [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

The `totalAmount` however may not represent the [full landed cost](landed-costs.md#what-is-landed-cost) of a transaction. That depends on how you configure a checkout's [`shippingChoice.shippingTerms`](shipping-choice.md#shipping-terms).

If a [checkout triggers the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature-1), then `importerOfRecordTax` returns `true`. In these cases, `totalImporterTax` indicates the tax amount that the importer of record remits to the government and `totalDuty` are duties levied on the products by the importing country.

{% hint style="warning" %}
Sometimes products in a [cross-border](../../../general-resources/glossary.md#cross-border) transaction don't incur any duties. As a result, in [checkouts that trigger the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature), `totalDuty` is not always greater than zero.
{% endhint %}

A [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `totalTax` represents taxes that Digital River remits to the government. Its value does not include `totalImporterTax`. Those taxes are remitted to the government by your shipper.

This means that a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `subtotal` includes `totalImporterTax` but doesn't include `totalTax`.

### Line item level attributes <a href="#item-level-attributes" id="item-level-attributes"></a>

In [checkouts that trigger the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature), each element in [`items[]`](describing-the-items/) contains three landed cost-related attributes:

#### Importer tax amount

The `importerTax.amount` indicates the amount of taxes that the importer of record pays on all the products in this line item.

#### Duties amount

The `duties.amount` indicates the amount of duty levied by an importing country on all the products in this line item.

#### Tariff code

A `tariffCode` represents a product's country-specific [Harmonized System code](https://www.trade.gov/harmonized-system-hs-codes). This value is only returned if you're using [SKU groups](../../../product-management/setting-up-sku-groups.md).

Landed cost calculations are based on this `tariffCode`. As a result, it's often useful for troubleshooting purposes. For example, if [cross-border](../../../general-resources/glossary.md#cross-border) duties presented to the customer during checkouts are later determined to be inaccurate, you can verify whether the correct code was applied to the product.

## European Union cross-border threshold

In the European Union, there’s a de minimis threshold, currently set at 150 EUR, that determines whether (1) duties are collected on imported goods and (2) the buyer or seller is responsible for remittances.

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) where goods are being shipped [cross-border](../../../general-resources/glossary.md#cross-border) into the EU, Digital River’s tax service determines whether the aggregated, intrinsic `price` of its [physical](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) `items[]`, excluding `shippingChoice.amount`, is (A) [less than or equal to](landed-costs.md#less-than-or-equal-to-the-threshold) or (B) [greater than](landed-costs.md#greater-than-the-threshold) this threshold.

### Less than or equal to the threshold

If it’s less than or equal to the 150 EUR threshold, then:

* `totalDuty` is `0`, because duties aren’t collected on what the EU considers to be low-value imports.
* `Digital River Ireland Ltd.`, the [`sellingEntity.name`](selling-entities.md) assigned to the transaction, is responsible for the remittance of value-added tax.
* `totalTax` contains the amount that this selling entity must remit, which is added to the `totalAmount` that the buyer pays.
* Each `items[]` is assigned a `sellerTaxIdentifier`, which represents Digital River’s [Import One-Stop Shop](https://en.wikipedia.org/wiki/Import\_One-Stop\_Shop) registration number. After the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) is converted to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), this value should be added to the [commercial invoice](https://en.wikipedia.org/wiki/Commercial\_invoice) to ensure that buyers aren’t assessed taxes again by customs (i.e., double-charged).

{% tabs %}
{% tab title="POST /checkouts" %}
```
curl --location 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret API key>' \
....
--data-raw '{
    "currency": "EUR",
    ...
    "taxInclusive": false,
    "shipTo": {
        ...
        "address": {
            "line1": "Deinsesteenweg 108B",
            "city": "Drongen",
            "postalCode": "9031",
            "state": "Oost-Vlaanderen",
            "country": "BE"
        }
    },
    "shipFrom": {
        "address": {
            "line1": "5215 4th Ave S",
            "city": "Minneapolis",
            "postalCode": "55104",
            "state": "MN",
            "country": "US"
        }
    },
    "items": [
        {
            "skuId": "sku_7d8c3133-342a-4c8e-90b2-ac541fcccd13",
            "price": 75,
            "quantity": 1
        },
        {
            "skuId": "sku_00af8f73-4aa6-4b08-b904-78b42869da73",
            "price": 75,
            "quantity": 1
        }
    ]
}'
```
{% endtab %}

{% tab title="201 Created" %}
```json
{
    "id": "b83bb92f-f5b5-40d0-9d6d-59a9968d5d83",
    ...
    "currency": "EUR",
    ...
    "shipTo": {
        "address": {
            "line1": "Deinsesteenweg 108B",
            "city": "Drongen",
            "postalCode": "9031",
            "state": "Oost-Vlaanderen",
            "country": "BE"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "line1": "5215 4th Ave S",
            "city": "Minneapolis",
            "postalCode": "55104",
            "state": "MN",
            "country": "US"
        }
    },
    "totalAmount": 181.5,
    "subtotal": 150.0,
    ...
    "totalTax": 31.5,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    ...
    "items": [
        {
            "id": "21a44c0f-a50b-43bf-91a6-ebb8d63fbe03",
            "skuId": "sku_7d8c3133-342a-4c8e-90b2-ac541fcccd13",
            ...
            "amount": 75.0,
            "quantity": 1,
            "tax": {
                "rate": 0.21,
                "amount": 15.75
            },
            "importerTax": {},
            "duties": {},
            ...
            "sellerTaxIdentifier": "IM3720000202",
            ...
        },
        {
            "id": "0d99a3a7-2601-4980-8fa9-af5cf1d9f3e0",
            "skuId": "sku_00af8f73-4aa6-4b08-b904-78b42869da73",
            ...
            "amount": 75.0,
            "quantity": 1,
            "tax": {
                "rate": 0.21,
                "amount": 15.75
            },
            "importerTax": {},
            "duties": {},
            ...
            "sellerTaxIdentifier": "IM3720000202",
            ...
        }
    ],
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

### Greater than the threshold

If the aggregated value of the imported goods is greater than the 150 EUR threshold, then:

* Buyers are responsible for the remittance of tax and duty.
* Assuming your account has the [landed cost feature](landed-costs.md#digital-rivers-landed-cost-feature) enabled and you don’t set the [checkout’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.shippingTerms` to `DAP`, the amount that the buyer must remit is assigned to `totalImporterTax` and `totalDuty`.
* `totalImporterTax` and `totalDuty` are added to `totalAmount`, which means `Digital River Ireland Ltd.`, the [`sellingEntity.name`](selling-entities.md) assigned to the transaction, is collecting these costs, in advance, on behalf of the buyer and then remitting them later.

{% tabs %}
{% tab title="POST /checkouts" %}
```
curl --location 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret API key>' \
....
--data-raw '{
    "currency": "EUR",
    ...
    "taxInclusive": false,
    "shipTo": {
        ...
        "address": {
            "line1": "Deinsesteenweg 108B",
            "city": "Drongen",
            "postalCode": "9031",
            "state": "Oost-Vlaanderen",
            "country": "BE"
        }
    },
    "shipFrom": {
        "address": {
            "line1": "5215 4th Ave S",
            "city": "Minneapolis",
            "postalCode": "55104",
            "state": "MN",
            "country": "US"
        }
    },
    "items": [
        {
            "skuId": "sku_7d8c3133-342a-4c8e-90b2-ac541fcccd13",
            "price": 75,
            "quantity": 1
        },
        {
            "skuId": "sku_00af8f73-4aa6-4b08-b904-78b42869da73",
            "price": 76,
            "quantity": 1
        }
    ]
}'
```
{% endtab %}

{% tab title="201 Created" %}
```json
{
    "id": "8365ecbc-0e28-4ba4-bcc7-75ae8c6a93f4",
    ...
    "currency": "EUR",
    ...
    "shipTo": {
        "address": {
            "line1": "Deinsesteenweg 108B",
            "city": "Drongen",
            "postalCode": "9031",
            "state": "Oost-Vlaanderen",
            "country": "BE"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "line1": "5215 4th Ave S",
            "city": "Minneapolis",
            "postalCode": "55104",
            "state": "MN",
            "country": "US"
        }
    },
    "totalAmount": 213.77,
    "subtotal": 213.77,
    ...
    "totalTax": 0.0,
    "totalImporterTax": 37.1,
    "importerOfRecordTax": true,
    "totalDuty": 25.67,
    ...
    "items": [
        {
            "id": "b8408be2-9abf-42dd-b4ff-1e36e1d776a4",
            "skuId": "sku_7d8c3133-342a-4c8e-90b2-ac541fcccd13",
            ...
            "amount": 75.0,
            "quantity": 1,
            "tax": {
                "rate": 0.38,
                "amount": 0.0
            },
            "importerTax": {
                "amount": 18.43
            },
            "duties": {
                "amount": 12.75
            },
            ...
        },
        {
            "id": "8b6c522a-2751-44bb-af07-a68147746b72",
            "skuId": "sku_00af8f73-4aa6-4b08-b904-78b42869da73",
            ...
            "amount": 76.0,
            "quantity": 1,
            "tax": {
                "rate": 0.38,
                "amount": 0.0
            },
            "importerTax": {
                "amount": 18.67
            },
            "duties": {
                "amount": 12.92
            },
            ...
        }
    ],
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

