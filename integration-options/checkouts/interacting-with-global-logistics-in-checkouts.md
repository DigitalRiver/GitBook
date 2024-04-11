---
description: >-
  If you've selected the Direct Integrations option, gain a better understanding
  of how to interact with Global Logistics in checkouts
---

# Interacting with Global Logistics in checkouts

If you implement a [Direct Integration](./) checkout solution and enable [Global Logistics](../../using-our-services/global-logistics.md), this page contains an [overview of how to manage the checkout process](interacting-with-global-logistics-in-checkouts.md#overview). You'll also find details on how to:

* [Build a cart](interacting-with-global-logistics-in-checkouts.md#building-a-cart)
* [Handle ship to country restrictions](interacting-with-global-logistics-in-checkouts.md#handling-ship-to-country-restrictions)
* [Manage shipping quotes](interacting-with-global-logistics-in-checkouts.md#managing-shipping-quotes)
* [Collect payment ](interacting-with-global-logistics-in-checkouts.md#collecting-payment)
* [Submit the order](interacting-with-global-logistics-in-checkouts.md#submitting-the-order)

## Overview

During checkouts, Digital River's [Global Logistics](../../using-our-services/global-logistics.md) (GL) service gives you the capability to [request international shipping quotes](interacting-with-global-logistics-in-checkouts.md#defining-and-sending-the-shipping-quote-request). Digital River routes your request to the appropriate [global logistics provider](../../using-our-services/global-logistics.md#global-logistics-providers) (GLP) and then uses their response to provide you with a [menu of shipping options](interacting-with-global-logistics-in-checkouts.md#successful-shipping-quotes-response) that you can [optionally filter](interacting-with-global-logistics-in-checkouts.md#filtering-and-adjusting-shipping-quotes) and then [display to customers](interacting-with-global-logistics-in-checkouts.md#displaying-shipping-quotes).

Once customers select a shipping quote, [apply their choice to the checkout](interacting-with-global-logistics-in-checkouts.md#handling-the-shipping-quote-selection), and then, assuming they selected a quote with [delivered duty paid](interacting-with-global-logistics-in-checkouts.md#shipping-terms) (DDP) terms, use the duty, fee, and import tax amounts returned by Digital River to present customers with a transaction's [full landed cost](creating-checkouts/landed-costs.md#what-is-landed-cost).

## Building a cart

During the early stages of an ecommerce transaction, customers land on your storefront, review products, build a cart, confirm the cart's details, and initiate checkout. This cart-building process is roughly the same for both domestic and international transactions.

However, some of your products might have country restrictions applied to them. In other words, products which are prohibited from being imported into certain countries.

To handle this, you might want to block customers from adding restricted products to their carts. This helps avoid issues at customs as well as unanticipated return costs.

Plug-ins and extensions exist that geo-locate a customer's country. These add-ons then hide products from customers who are located in restricted countries. Some of these extensions allow you to disable the add-to-cart button for prohibited product-country combinations.

## Creating the checkout

However you [send product data in create checkout requests](creating-checkouts/describing-the-items/#sending-product-data), make sure each [physical](../../product-management/skus.md#how-to-identify-a-physical-or-digital-sku) `items[]` has a name, description, weight, image, and url. For details, refer to [Defining basic product data](../../using-our-services/global-logistics.md#defining-basic-product-data) on the [Global Logistics](../../using-our-services/global-logistics.md) page.

## Handling ship to country restrictions

Once you initiate checkout, you should obtain the customer's name, email, shipping address, and billing address.

For details, refer to [sequencing the checkout process](creating-checkouts/#sequencing-the-checkout-process) on the [Building checkouts](creating-checkouts/) page.

When collecting a customer's shipping information in your checkout experience, we suggest using a drop-down menu (or a similar graphical control element) that restricts available ship to countries to those defined by your [trading patterns](../../using-our-services/global-logistics.md#defining-trading-patterns), plus any additional countries you may be shipping to with the help of another logistics service.

## Managing shipping quotes

Once you collect the customer's ship to information, [define and send a shipping quotes request](interacting-with-global-logistics-in-checkouts.md#defining-and-sending-the-shipping-quote-request) to Digital River. We transform your request and route it to the appropriate [global logistics provider](../../using-our-services/global-logistics.md#global-logistics-providers) (GLP). The quality of the data you provide in this request determines the accuracy of the returned shipping quotes.

Upon receiving a [successful shipping quote response](interacting-with-global-logistics-in-checkouts.md#successful-shipping-quotes-response), you could [handle the response](interacting-with-global-logistics-in-checkouts.md#handling-the-shipping-quotes-response) by [applying a filter](interacting-with-global-logistics-in-checkouts.md#filtering-and-adjusting-shipping-quotes) before [displaying the quotes to customers](interacting-with-global-logistics-in-checkouts.md#displaying-shipping-quotes). Once the customer makes a selection, [handle that event](interacting-with-global-logistics-in-checkouts.md#handling-the-shipping-quote-selection) by retrieving data from the selected quote and using it to update the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

### Defining and sending the shipping quote request

A [`POST /shipping-quotes`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShippingQuotes) request must pass a [currency](interacting-with-global-logistics-in-checkouts.md#currency), [ship to address](interacting-with-global-logistics-in-checkouts.md#ship-to), as well as [product and package data.](interacting-with-global-logistics-in-checkouts.md#packaging-and-product-data)

```powershell
curl --location 'api.digitalriver.com/shipping-quotes' \
--header 'Authorization: Bearer sk_test_343ddc5696e741b9b72a25de50f49ee6' \
--header 'Content-Type: application/json' \
--header 'Cookie: incap_ses_2101_1638494=tN70L9jJWwuBbqCbn0AoHWEwI2QAAAAARBWkgVilEwQuQA+kNZLVZQ==; nlbi_1638494_1914372=JivDUiucpRTFcbaKiXZ5LAAAAADW8KH8Q0zsipzOaOkg+Sdf; visid_incap_1638494=F+YbmPRBQV6qjnK2EapeH32gIWQAAAAAQUIPAAAAAAD7C2DNNcFOo7+iTjx6f0LK; Cookie_6=BIGipServerp-c020-gc-ica-admin-dc2-a1-active=293148426.64288.0000; Cookie_7=BIGipServerp-c020-gc-ica-shopper-dc2-s1-active=444143370.64288.0000; Cookie_8=BIGipServerp-c021-gc-sca-odsshopper-dc2-o1-active=!OhjDMSomDcB2YEE1x8Vl8DId3ryVdxpPZPmuV6tbSfGv17BizaNrIRaW4pTWy7BeqhvVFV02Ara7BjQ=; Cookie_9=BIGipServerp-c021-gc-sca-shopper-dc2-s1-s2-active=!vi0p5t6UvfLXzeo1x8Vl8DId3ryVd8qQ2Qj3wKSsTFhQVMTxblte8K+IRmdWrlhz+bFiRUk6ITpChfE=' \
--data-raw '{
    "currency": "USD",
    "shipTo": {
        "address":{
            "line1": "96 Euston Rd",
            "city": "London",
            "postalCode": "98001",
            "country": "IT"
        },
        "name": "C. Brown",
        "phone": "330-333-1144",
        "email": "jchou@digitalriver.com"
    },
    "packages": [
        {
            "items": [
                {
                    "productDetails": {
                        "id": "upsid_1680034693",
                        "skuGroupId": "group_9c99cdf6-3a36-462d-96da-a96c4f003c43",
                        "name": "phy_N1_1679494194",
                        "description": "Top rated keyboard",
                        "url": "https://producturl.com",
                        "countryOfOrigin": "US",
                        "image": "https://imageurl.com",
                        "partNumber": "DEMOPARTNUMBER2"
                    },
                    "amount": 7.99,
                    "quantity": 1
                }
            ], 
            "weight": 10.5,
            "weightUnit": "lb"
        }
    ]
}'
```

#### Currency

The cost of each returned shipping quote is converted into this `currency`. It should be the same value as the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`currency`](creating-checkouts/selecting-a-currency.md).&#x20;

#### Ship to

Earlier in the checkout process, you required customers to select a ship to country from a [restricted list](interacting-with-global-logistics-in-checkouts.md#handling-ship-to-country-restrictions). You also obtained the customer's ship to street address, city, state/region, and postal code.

Retrieve these same values and pass them in the request's `shipTo`. This helps make the returned shipping quotes as accurate as possible. However, the only hard requirement in `shipTo` is `address.country`.&#x20;

#### Ship from

The request's `shipFrom` represents the address of the product's warehouse. It's not a requirement because Global Logistics identifies the appropriate [trading pattern](../../using-our-services/global-logistics.md#defining-trading-patterns) by using the request's [`shipTo.address.country`](interacting-with-global-logistics-in-checkouts.md#ship-to).&#x20;

#### Packaging and product data

Your request must contain information on the `packages[]` being shipped and the `items[]` within each. In multi-package transactions, this allows you to designate which products will be sent in each parcel, potentially making the returned shipping rates more precise.&#x20;

If you have a [dynamic packing integration with your WMS](../../using-our-services/global-logistics.md#packing-algorithms), before sending the `POST/ shipping-quotes`, you could call that service and provide it data on the [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) in the customer's cart so that its algorithms can tell you the optimal number of `packages[]`, the `weight`, `height`, `width`, and `length` of each, plus which `items[]` should go in those `packages[]` and then send that data to Digital River in the request.&#x20;

Additionally, you might have large products which you know are always packaged individually. In this case, for each of these product types, you can send one `packages[]` with a single `items[]` with a `quantity` of `1`.&#x20;

For each `packages[]`:

* Its `height`, `width`, and `length` should be represented in inches.&#x20;
* If you don’t pass a `height`, `width`, or `length`, Global Logistics looks for these values in your [default package settings](../../using-our-services/global-logistics.md#default-box). If you have no saved dimensions, we pass a `height`, `width`, and `length` of one inch to the [GLP](../../using-our-services/global-logistics.md#global-logistics-providers).
* If you don't pass `weight`, we look for values in `items[].productDetails.weight`. However, if you do define this parameter in `packages[]`, we ignore any `weight`(s) in `productDetails`.

{% hint style="success" %}
For details on why it's important that the quote request that Digital River routes to the designated [GLP](../../using-our-services/global-logistics.md#global-logistics-providers) contains weight values, refer to [Product weight and dunnage. ](../../using-our-services/global-logistics.md#defining-basic-product-data)
{% endhint %}

For each `items[]` in that `packages[]`:

* You need to send its [`productDetails`](../../product-management/using-product-details.md).&#x20;
  * The `id` should reference the product in your order management system.
  * The required `skuGroupId`  must reference the [SKU group](../../product-management/setting-up-sku-groups.md) that the product belongs to. From this resource, we retrieve the [product's compliance data](../../using-our-services/global-logistics.md#defining-compliance-product-data). &#x20;
  * The product's `weight`. If you don’t pass `weight` in `productDetails`, we look for a weight in your [default package settings](../../using-our-services/global-logistics.md#configuring-packaging). If you have no saved value, we send a `weight` of one pound to the GLP.&#x20;

{% hint style="info" %}
For both `packages[]` and `items[].productDetails`, the enumerated values of `weightUnit` are `oz`, `lb`, `g`, and `kg`. The default value is `lb`.
{% endhint %}

* You're required to specify a `quantity`. This is a key input for accurately calculating shipping rates.

### How your request gets processed

Digital River retrieves product and packaging data from your [shipping quotes request](interacting-with-global-logistics-in-checkouts.md#defining-and-sending-the-shipping-quote-request) and uses it to define another request that we route to the appropriate [GLP](../../using-our-services/global-logistics.md#global-logistics-providers). We also determine whether any products in the request are [classified as dangerous goods](../../using-our-services/global-logistics.md#dangerous-goods-classifications) and/or [require a signature](../../using-our-services/global-logistics.md#signature-requirements), and, if this is the case, pass that data to the GLP.

When the [GLP](../../using-our-services/global-logistics.md#global-logistics-providers) responds to our request with a list of quotes, we convert the cost of each back into the same [`currency`](interacting-with-global-logistics-in-checkouts.md#currency) you specified in your request. For each quote returned by the GLP, we also aggregate any carrier-assessed fees and surcharges into a [single total amount](interacting-with-global-logistics-in-checkouts.md#shipping-costs-and-fees).

### Successful shipping quotes response

A successful `POST /shipping-quotes` request returns a `currency` and an array of shipping `quotes[]`.

The `currency` is always the same value that you sent in the request.

{% code title="200" %}
```json
{
    "currency": "CAD",
    "quotes": [
        {
            "id": "58SLC-DHL",
            "description": "Express",
            "estimatedDelivery": "3 - 5 Business Days",
            "shippingTerms": "DDP",
            "totalAmount": 28.19,
            "shipFrom": {
                "address": {
                    "city": "Salt Lake City",
                    "postalCode": "84604",
                    "state": "Utah",
                    "country": "US"
                }
            },
            "fees": {
                "details": [
                    {
                        "name": "Fuel Surcharge",
                        "amount": 1.72
                    },
                    {
                        "name": "Temporary Surcharge",
                        "amount": 0.45
                    },
                    {
                        "name": "Dangerous Goods Fee",
                        "amount": 1.56
                    }
                ],
                "amount": 3.72
            }
        },
        {
            "id": "58SLC-DHL",
            "description": "Express",
            "shippingTerms": "DAP",
            "totalAmount": 28.19,
            "shipFrom": {
                "address": {
                    "city": "Salt Lake City",
                    "postalCode": "84604",
                    "state": "Utah",
                    "country": "US"
                }
            },
            "fees": {
                "details": [
                    {
                        "name": "Fuel Surcharge",
                        "amount": 1.72
                    },
                    {
                        "name": "Temporary Surcharge",
                        "amount": 0.45
                    },
                    {
                        "name": "Dangerous Goods Fee",
                        "amount": 1.56
                    }
                ],
                "amount": 3.72
            }
        }
    ],
    "liveMode": false
}
```
{% endcode %}

Each element in `quotes[]` contains the following attributes:

#### Unique identifier

Each `quotes[]` has a unique `id`, which is generated by the [GLP](../../using-our-services/global-logistics.md#global-logistics-providers).

This `id` doesn't reference a resource, so you can't use it to make an API call to retrieve a unique shipping quote.

When [handling a customer's shipping quote selection](interacting-with-global-logistics-in-checkouts.md#handling-the-shipping-quote-selection), use the selected quote's `id` to define the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.id`. If you don't perform this operation, then the downstream [create shipping label request](../../order-management/managing-a-global-logistics-order.md#managing-shipping-labels) will fail.

#### Description

The `description` indicates the duration of transportation. In other words, how quickly the goods are transported to the customer and what priority level they are assigned. Some common values are `Economy`, `Express`, and `Priority`. This is a pass-thru value from the [GLP](../../using-our-services/global-logistics.md#global-logistics-providers).

#### Estimated delivery range

A shipping quote's `estimatedDelivery` defines a minimum and maximum delivery period in days. For example, `estimatedDelivery` might be `3 - 5 Business Days`.

#### Shipping terms

A quote's `shippingTerms` are designated as either `DDP` or `DAP`. These values indicate when customers must pay duties, fees, and import taxes.

In delivered-duty-paid (`DDP`) shipments, customers pays all duties, fees, and import taxes upfront during the checkout process. Upon product delivery, there are no additional charges they must pay.

In delivered-at-place (`DAP`) shipments, customers do _not_ pay the full landed cost at checkout-time. Instead, they pay product and shipping costs, and then, upon delivery, they're responsible for paying duties, fees, and import taxes.

#### Shipping costs and fees

The `totalAmount` of a `quotes[]` represents how much customers must pay to ship the goods to their final destination. It includes the estimated cost of handling, transportation, and postage as well as carrier-assessed surcharges and fees.

In `fees`, we itemize these estimated fees and surcharges. A carrier might collect them to, for example, offset the cost of higher fuel prices, package signature options, or dangerous goods handling requirements.

Each quote's `totalAmount`, `fees.amount`, and `fees.details[].amount` is denominated in the response's single `currency`.

#### Ship from

Each shipping quote's `shipFrom` represents the address where that product is warehoused.

If you maintain multiple warehouses in the same country, then the response might contain one or more `quotes[]` with the same `shipFrom.address.country` but other attributes nested in `shipFrom.address` (such as `line1` and `city`) that contain non-matching values.

### Failure response

You'll receive an error if you fail to define parameters marked as required in the [shipping quote request specifications](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes/operation/postShippingQuotes).&#x20;

In addition, if the request contains `shipFrom.address.country` and `shipTo.address.country` values not supported by your [trading patterns](../../using-our-services/global-logistics.md#defining-trading-patterns), we return a `400 Bad Request`.

```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "shipTo.address",
            "message": "The shipTo.address is invalid with the shipFrom.address"
        }
    ]
}
```

### Handling the shipping quotes response

Depending on your business objectives, you may decide you want to [filter and adjust the returned shipping quotes](interacting-with-global-logistics-in-checkouts.md#filtering-and-adjusting-shipping-quotes) before [displaying them to customers](interacting-with-global-logistics-in-checkouts.md#displaying-shipping-quotes).

#### Filtering and adjusting shipping quotes

By only displaying `quotes[]` whose `shippingTerms`  are `DDP`, you can help **minimize rejections, returns, and chargebacks**.\
\
Shipments with `DAP` terms generally have higher return rates. At the time of delivery, some customers may be unaware of the outstanding balance and, in response, either refuse the delivery altogether or accept the delivery and then return the products.\
\
However, you should be aware that some carriers and ship to country combinations don't support the prepay `DDP` option. In these cases, the only `quotes[]` in a [successful response](interacting-with-global-logistics-in-checkouts.md#successful-shipping-quotes-response) are those with `shippingTerms` of `DAP`. So, if one of your [ship to countries](../../using-our-services/global-logistics.md#defining-trading-patterns) doesn't support `DDP`, make sure you have logic in place that displays `DAP` quotes in the event `DDP` quotes are not returned.

If you'd like to **offer your customers a discount on shipping costs**, you can reduce one or more [`quotes[].totalAmount`](interacting-with-global-logistics-in-checkouts.md#shipping-costs-and-fees) values before [displaying them to customers](interacting-with-global-logistics-in-checkouts.md#displaying-shipping-quotes). Just make sure you pass this reduced amount when [setting the checkout's `shippingChoice`](interacting-with-global-logistics-in-checkouts.md#handling-the-shipping-quote-selection).

#### Displaying shipping quotes

For each shipping quote that you display to customers in your checkout UI, reveal its `serviceLevel`, `estimatedDelivery`, and `totalAmount`.

If you'd like to provide customers with more shipping cost granularity, you can also display `fees.details[]` and/or `fees.amount`.

In addition, you should indicate whether the quote's [`shippingTerms`](interacting-with-global-logistics-in-checkouts.md#shipping-terms) are `DAP` or `DDP`. However, we recommend not displaying these acronyms in your UI. Few, if any, customers will understand their meaning. Instead, display a more user-friendly description. For example:

| Shipping term | Customer-facing text                     |
| ------------- | ---------------------------------------- |
| `DAP`         | Import charges collected upon delivery   |
| `DDP`         | No additional import charges at delivery |

Here's an example of what this might look like:

![](<../../.gitbook/assets/Both DDP and DDP quotes (3).png>)

### Handling the shipping quote selection

When customers select a shipping quote, handle that event by retrieving the following data from their selection and using it to define [`shippingChoice`](creating-checkouts/shipping-choice.md) and [`shipFrom`](creating-checkouts/providing-address-information.md#ship-from-address) in an [update checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts):

| Shipping quote  |       | POST /checkouts/{id}           |
| --------------- | :---: | ------------------------------ |
| `id`            | **➔** | `shippingChoice.id`            |
| `amount`        | **➔** | `shippingChoice.amount`        |
| `description`   | **➔** | `shippingChoice.description`   |
| `serviceLevel`  | **➔** | `shippingChoice.serviceLevel`  |
| `shippingTerms` | **➔** | `shippingChoice.shippingTerms` |
| `shipFrom`      | **➔** | `shipFrom`                     |

This request prompts Digital River to call its landed cost service if all the [necessary preconditions](creating-checkouts/landed-costs.md#triggering-the-landed-cost-feature) are met,.

If the checkout's [`shippingTerms`](creating-checkouts/shipping-choice.md#shipping-terms) are [`DDP`](creating-checkouts/shipping-choice.md#delivered-duty-paid-ddp), then the response to your request provides recalculated duty, fee, and import tax amounts at both the checkout level and `items[]` level.

For details, refer to [how landed cost is represented in checkouts](creating-checkouts/landed-costs.md#how-landed-cost-is-represented) on the [Landed cost](creating-checkouts/landed-costs.md) page.

{% hint style="warning" %}
In the Global Logistics solution, the customer is the designated [importer of record](../../general-resources/glossary.md#importer-of-record). As a result, the customer pays the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `totalImporterTax`.
{% endhint %}

If the checkout's [`shippingTerms`](creating-checkouts/shipping-choice.md#shipping-terms) are [`DAP`](creating-checkouts/shipping-choice.md#delivered-at-place-dap), then checkout-level and `items[]` level duty, fee, and import tax amounts are all zero.

{% tabs %}
{% tab title="DDP Checkout" %}
```javascript
{
    "id": "206bfba3-7bda-4d0b-b6e3-657875b5cc6c",
    "createdTime": "2021-11-11T22:25:24Z",
    "currency": "EUR",
    "email": "jsmith@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "Neuer Wall 10",
            "city": "Hamburg",
            "postalCode": "20354",
            "country": "DE"
        },
        "name": "John",
        "phone": "9526123456",
        "email": "john@digitalriver.com"
    },
    "shipFrom": {
        "address": {
            "line1": "Landed Cost Cross Order",
            "line2": "80 Sunraysia Road",
            "city": "INVERMAY",
            "postalCode": "3352",
            "state": "Victoria",
            "country": "AU"
        }
    },
    "totalAmount": 1809.99,
    "subtotal": 1809.99,
    "totalFees": 0.0,
    "totalTax": 0.0,
    "totalImporterTax": 288.99,
    "importerOfRecordTax": true,
    "totalDuty": 221.0,
    "totalDiscount": 0.0,
    "totalShipping": 100.0,
    "items": [
        {
            "id": "434e3932-a20d-49d3-ad82-0abb25eaa9be",
            "skuId": "3c99757b-a543-455f-bbd3-57dc1bb21579",
            "amount": 1200.0,
            "quantity": 3,
            "tax": {
                "rate": 0.36,
                "amount": 0.0
            },
            "importerTax": {
                "amount": 288.99
            },
            "duties": {
                "amount": 221.0
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            },
            "tariffCode": "6404201000"
        }
    ],
    "shippingChoice": {
        "id": "testDDP",
        "amount": 100.0,
        "description": "FedEx Next Day",
        "serviceLevel": "Test",
        "taxAmount": 0.0,
        "shippingTerms": "DDP"
    },
    "updatedTime": "2021-11-11T22:25:24Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "liveMode": false,
    "payment": {
        "session": {
            "id": "1822d8bd-1531-40da-aedc-10ac9b0eda4c",
            "amountContributed": 0.0,
            "amountRemainingToBeContributed": 1809.99,
            "state": "requires_source",
            "clientSecret": "1822d8bd-1531-40da-aedc-10ac9b0eda4c_4b58e8ed-505c-4334-b349-bc65be9029e5"
        }
    }
}
```
{% endtab %}

{% tab title="DAP Checkout" %}
```javascript
{
    "id": "2554c935-98a4-49e6-95ac-1d179c47b2e4",
    "createdTime": "2021-11-11T22:26:22Z",
    "currency": "EUR",
    "email": "jsmith@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "Neuer Wall 10",
            "city": "Hamburg",
            "postalCode": "20354",
            "country": "DE"
        },
        "name": "John",
        "phone": "9526123456",
        "email": "john@digitalriver.com"
    },
    "shipFrom": {
        "address": {
            "line1": "Landed Cost Cross Order",
            "line2": "80 Sunraysia Road",
            "city": "INVERMAY",
            "postalCode": "3352",
            "state": "Victoria",
            "country": "AU"
        }
    },
    "totalAmount": 1300.0,
    "subtotal": 1300.0,
    "totalFees": 0.0,
    "totalTax": 0.0,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 100.0,
    "items": [
        {
            "id": "5fbe0052-7b63-460a-a5f6-c516ab9b900d",
            "skuId": "3c99757b-a543-455f-bbd3-57dc1bb21579",
            "amount": 1200.0,
            "quantity": 3,
            "tax": {
                "rate": 0.0,
                "amount": 0.0
            },
            "importerTax": {},
            "duties": {},
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            },
            "tariffCode": "6404201000"
        }
    ],
    "shippingChoice": {
        "id": "testDAP",
        "amount": 100.0,
        "description": "FedEx Next Day",
        "serviceLevel": "Test",
        "taxAmount": 0.0,
        "shippingTerms": "DAP"
    },
    "updatedTime": "2021-11-11T22:26:22Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "liveMode": false,
    "payment": {
        "session": {
            "id": "561f72d9-44e0-4002-840b-908df73926c4",
            "amountContributed": 0.0,
            "amountRemainingToBeContributed": 1300.0,
            "state": "requires_source",
            "clientSecret": "561f72d9-44e0-4002-840b-908df73926c4_3493ddf5-d60e-474d-b2d3-2bda3237649d"
        }
    }
}
```
{% endtab %}
{% endtabs %}

In both [`DAP`](creating-checkouts/shipping-choice.md#delivered-at-place-dap) and [`DDP`](creating-checkouts/shipping-choice.md#delivered-duty-paid-ddp) scenarios, use the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) data to update the product, shipping, duties, fees, taxes, and total amounts displayed to customers. When displaying duty and import tax amounts in `DAP` scenarios, let customers know they don't pay these costs at checkout time. We recommend using language such as "Outstanding" or "Collected upon delivery".

Here's an example of what this might look like:

{% tabs %}
{% tab title="DDP selection" %}
![](<../../.gitbook/assets/DDP selection (1).png>)
{% endtab %}

{% tab title="DAP selection" %}
![](<../../.gitbook/assets/DAP selection.png>)
{% endtab %}
{% endtabs %}

## **Collecting payment**

In [Global Logistics](../../using-our-services/global-logistics.md), you collect payment in the same way you would in any [checkout flow](creating-checkouts/).

Before initiating the payment collection process, you obtain the customer's billing information and use it to set (at a minimum) the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`billTo.address.country`](creating-checkouts/providing-address-information.md#bill-to-address).&#x20;

Once you initiate payment collection, [Drop-in payments](../../payments/payment-integrations-1/drop-in/) only display payment methods applicable to that currency and bill to country.

If you're using [DigitalRiver.js with elements](../../payments/payment-integrations-1/digitalriver.js/quick-start.md) to collect payment, make sure that only applicable payment methods are presented to customers by calling [`retrieveAvailablePaymentMethods()`](../../developer-resources/reference/digitalriver-object.md#retrieving-available-payment-methods).

For details, refer to:

* The [Drop-in integration guide](../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md)
* The [DigitalRiver.js quick start guide](../../payments/payment-integrations-1/digitalriver.js/quick-start.md)
* The [Building your payment workflows](building-you-workflows/) page
* The [Managing sources](../../payments/payment-sources/using-the-source-identifier.md) page

## Submitting the order

Once the necessary preconditions are met, you can [convert the checkout to an order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). After the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) either [synchronously](../../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) moves to `accepted`, [send a ship request](../../order-management/managing-a-global-logistics-order.md#sending-the-ship-request) to your [third-party logistics](../../general-resources/glossary.md#third-party-logistics) (3PL) provider.

For details, refer to [Managing a Global Logistics order](../../order-management/managing-a-global-logistics-order.md).

