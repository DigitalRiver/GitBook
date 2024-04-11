---
description: >-
  Learn how to provide your customers shipping options and process their
  selection
---

# Using shipping quotes

{% hint style="warning" %}
This page explains how to use the [Shipping Quotes API](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/postShippingQuotes) in [versions](../../../general-resources/versioning.md) `2020-12-17`, `2020-02-23`, and `2021-03-23` as part of a [Digital River coordinated fulfillment](./).\
\
In versions `2021-12-13` and higher, the `/shipping-quotes` endpoint has been repurposed for use in our [Global logistics](../../../using-our-services/global-logistics.md) solution.
{% endhint %}

In [Digital River coordinated fulfillments](./), you call the [Shipping Quotes API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) during the [checkout process](../creating-checkouts/) to provide customers with shipping options.

In a [shipping quotes request](using-shipping-quotes.md#requesting-shipping-quotes), you must [describe the items](using-shipping-quotes.md#items-to-ship) you'd like to ship and [where those items are going](using-shipping-quotes.md#shipping-destination-and-type).

In the response, we give you back an array of [shipping quotes](using-shipping-quotes.md#shipping-quotes), each describing the quote's [service level](using-shipping-quotes.md#unique-identifier-and-service-levels), [shipping costs](using-shipping-quotes.md#shipping-costs), [signature requirements](using-shipping-quotes.md#signature-requirements), [estimated delivery times](using-shipping-quotes.md#estimated-delivery-times), [inventory availability](using-shipping-quotes.md#inventory-item-identifier-and-availability), and [ship from addresses](using-shipping-quotes.md#ship-from-addresses).

These shipping quotes can then be displayed to the customer. Once the customer selects, you can [use a shipping quote's data to continue processing the checkout](using-shipping-quotes.md#using-a-shipping-quote).

{% hint style="info" %}
In [third-party coordinated fulfillments](../../../order-management/fulfillments.md#third-party-coordinated-fulfillments), the checkout's [shipping information](../creating-checkouts/shipping-choice.md) must be obtained from your logistics partner.
{% endhint %}

## Requesting shipping quotes

In a [`POST/shipping-quotes`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShippingQuotes) request, you need to provide the `currency` used to pay for the shipping, the [items to ship](using-shipping-quotes.md#items-to-ship), and their [destination and delivery type](using-shipping-quotes.md#shipping-destination-and-type).

This call to the [Shipping Quotes API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) typically occurs late in the [checkout process](../creating-checkouts/), after customers have finalized their carts and you've collected their shipping address. So, much of the data you need to define the request can be retrieved from the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

| `Checkout`          |       | `POST/shipping-quotes`    |
| ------------------- | ----- | ------------------------- |
| `currency`          | **➔** | `currency`                |
| `items[].skuId`     | **➔** | `items[].inventoryItemId` |
| `items[].amount`    | **➔** | `items[].price`           |
| `items[].quantity`  | **➔** | `items[].quantity`        |
| `shipTo.postalCode` | **➔** | `shipTo.postalCode`       |
| `shipTo.state`      | **➔** | `shipTo.state`            |
| `shipTo.country`    | **➔** | `shipTo.country`          |

{% tabs %}
{% tab title="POST/shipping-quotes" %}
```
curl --location --request POST 'http://api.digitalriver.com/shipping-quotes' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "currency": "USD",
    "shipTo": {
        "postalCode": "11111",
        "state": "BU",
        "country": "JP",
        "type": "standard"
    },
    "items": [
        {
            "inventoryItemId": "78fd6209-91e7-4347-aadc-af73edb8b18b",
            "price": 9.99,
            "quantity": 1
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

### Items to ship

You must provide an array of products in your shipping quotes request. Each element of the `items` array represents a specific [inventory item](../../../product-management/skus.md#inventory-items). For each inventory item, you're required to specify its unique identifier, `price`, and `quantity`.

{% hint style="warning" %}
In [Digital River coordinated fulfillments](./), your [SKUs and inventory items](../../../product-management/common-attributes.md) form synchronous pairs. So the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `items[].skuId` can be used to set the [shipping quotes'](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes)`items[].inventoryItemId`.
{% endhint %}

### Shipping destination and type

For Digital River to return accurate shipping quotes, you need to specify the `shipTo` block's `state`, `country`, and `postalCode`.

You can also use `shipTo` to set `type`. This parameter represents the final step in the fulfillment process, actually delivering the products to a customer. The `type` options are [`standard`](using-shipping-quotes.md#standard-deliveries)(_default_), [`access_point`](using-shipping-quotes.md#access-point-deliveries), or [`cash_on_delivery`](using-shipping-quotes.md#cash-on-delivery). The delivery `type` affects [the returned service levels](using-shipping-quotes.md#unique-identifier-and-service-levels).

#### Standard deliveries

A `standard` delivery type is the most common and consists of the shipping carrier bringing the goods directly to the customer's home or place of business.

#### Access point deliveries

With `access_point` deliveries, customers pick up their products at stand-alone lockers located in high-traffic areas like shopping centers and train stations. Alternatively, the goods can be delivered to so-called "parcel shops", such as convenience and grocery stores, where the customer picks them up.

#### Cash on delivery

When you specify `cash_on_delivery`, end customers must pay the shipping carrier for the goods at the time of delivery. This cash-on-delivery (COD) payment method is particularly popular in Japan, China, Mexico, Indonesia, Germany, Spain, Turkey, UAE, Russia and other countries.

If you set `type` to `cash_on_delivery`, once [physical fulfillment](global-fulfillments.md) is initiated, we send this data downstream to the fulfiller, who, in turn, notifies the shipping carrier to collect COD.

## Shipping quotes

A successful [`POST/shipping-quotes`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShippingQuotes) request returns a `quotes` array. Each object of that array represents a [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes). This object always contains a [unique identifier associated with a shipping service level](using-shipping-quotes.md#unique-identifier-and-service-levels), as well as information on [shipping costs](using-shipping-quotes.md#shipping-costs), where the [items are shipping from](using-shipping-quotes.md#ship-from-addresses), and [product availability](using-shipping-quotes.md#inventory-item-identifier-and-availability).

Depending on your configuration, you may also get back data on [signature requirements](using-shipping-quotes.md#signature-requirements) and [estimated delivery times](using-shipping-quotes.md#estimated-delivery-times).

### Unique identifier and service levels

Every [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) contains a unique `id` which is associated with a shipping method. This shipping method is designated by `serviceLevel`. That service level is, in turn, associated with the [delivery type](using-shipping-quotes.md#shipping-destination-and-type) you specify in the request.

{% tabs %}
{% tab title="Shipping quotes" %}
```javascript
{
    "shipTo": {
        ...
        "type": "standard"
    },
    "quotes": [
        {
            "id": "IC",
            ...
            "serviceLevel": "InternationalStandard",
            ...
            "total": 10.0,
            ...
        },
        {
            "id": "IS",
            ...
            "serviceLevel": "InternationalExpress",
            ...
            "total": 20.0,
            ...
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

The following table lists these enumerated shipping quote identifiers, their associated service levels, and the delivery type they support.

As an example, if you specify a [`shipTo.type`](using-shipping-quotes.md#shipping-destination-and-type) of `access_point` in the `POST/shipping-quotes` request, you'll get back a maximum of two shipping quotes. That is the number of service levels this delivery type supports.

| Identifier | Shipping service level  | Supported delivery type |
| ---------- | ----------------------- | ----------------------- |
| `A1`       | `accessPointExpress`    | `access_point`          |
| `AG`       | `accessPointStandard`   | `access_point`          |
| `D1`       | `expressNextDay`        | `standard`              |
| `D2`       | `expressSecondDay`      | `standard`              |
| `IH`       | `inHome`                | `standard`              |
| `IC`       | `internationalExpress`  | `standard`              |
| `IS`       | `internationalStandard` | `standard`              |
| `SG`       | `standard`              | `standard`              |
| `COD`      | `standardCOD`           | `cash_on_delivery`      |

### Shipping costs

A [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) provides you with order-level and item-level `shipping` and `handling` costs. We aggregate these amounts into both an item `total` and an order `total`.

We also give you information on any `fees` incurred for non-standard services that may have been applied to the order.

### Signature requirements

A [shipping quote's](using-shipping-quotes.md#requesting-shipping-quotes) `signatureRequiredType` indicates whether a signature is needed upon delivery and, if it is, what type of signature is required. It's commonly used to prevent the theft of high-dollar items from a customer's doorstep after the goods have been delivered.

The value indicates whether the shipping carrier requires an `adult` to sign for delivery or a `standard` signer of any age is acceptable.

If `signatureRequiredType` is not contained in the response, it means that no delivery confirmation is needed for any of the products in the shipping quote.

Shipping carriers typically charge for performing this signature collection service. If you decide to pass this cost on to customers, then the amount the carrier charged is reflected in `handling`.

On orders with split shipments, meaning items are going to different addresses or arriving at the same address at different times, `handling` indicates the total signature collection cost for all the different shipments.

The order shipped notification you send customers should indicate whether they must provide a signature upon delivery.

#### Enabling the signature required feature

You must contact your account manager to configure and enable the signature required feature.

The configuration process involves several steps. First, specific products within your channel's catalog need to be flagged. When these flagged products are included in an order, they trigger the signature required feature.

You can also set item-level and order-level amount thresholds. These tell us when to activate the feature. Let's say you have a product that is not flagged for signature collection. But a customer orders enough of these products to exceed your pre-defined amount threshold, triggering a mandatory signature collection.

And finally, you'll need to tell us whether you or the customer will pay the cost the shipping carrier charges for providing this service.

### Estimated delivery times

The `estimatedMinimumDeliveryTime` and `estimatedMaximumDeliveryTime` represent estimated minimum and maximum delivery times (in minutes) for this shipping method.

### Inventory item identifier and availability

For each item in a shipping quote, we provide you its `inventoryItemId` as well as its `quantity`, `availableQuantity`, and `availableTime`.

{% hint style="warning" %}
You can also retrieve this same data by making a [`GET/inventory-levels`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listInventoryLevels) request.
{% endhint %}

### Ship from addresses

In a [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes), each element of the `items` array provides you with a `shipFrom` address. This indicates the warehouse location where that specific product is shipped from. This allows you to [build checkouts with products that ship from different addresses in different countries](../creating-checkouts/providing-address-information.md#ship-from-address).

{% tabs %}
{% tab title="Shipping quotes" %}
```javascript
{
    ...
    "quotes": [
        {
            "id": "SG",
            ...
            "items": [
                {
                    "inventoryItemId": "f785a6ac-d37b-46ca-92ed-2bea6f9dd14a",
                    ...
                    "shipFrom": {
                        "address": {
                            "line1": "27081 Aliso Creek Rd",
                            "city": "Aliso Viejo",
                            "postalCode": "92656",
                            "state": "CA",
                            "country": "US"
                        }
                    },
                    ...
                }
            ]
        },
        ...
    ],
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

## Using a shipping quote

In [Digital River coordinated fulfillments](./) that use either the [distributed model](./#distributed-model) or [orchestrated model](./#orchestrated-model)**,** after you [receive an array of shipping quotes](using-shipping-quotes.md#shipping-quotes), present them to the customer.

Once the customer selects a specific shipping quote, retrieve its data and send it in a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkout request. This associates the shipping quote with the [checkout](using-shipping-quotes.md#requesting-shipping-quotes).

Specifically, you should retrieve the shipping quote's `id` and `total` and use these values to set the checkout's `shippingChoice.serviceLevel` and `shippingChoice.amount`.

If all of a [shipping quote's ship from values](using-shipping-quotes.md#ship-from-addresses) are identical, you can use this one address to specify [the checkout's `shipFrom`](../creating-checkouts/providing-address-information.md#specifying-ship-from-at-the-checkout-level). However, when [describing a checkout's items](../creating-checkouts/describing-the-items/), you have the ability to [set `shipFrom` at the line-item level](../creating-checkouts/providing-address-information.md#specifying-ship-from-at-the-item-level). So, if the shipping quote contains items with different ship from addresses, pass each of these unique values to the checkout's corresponding line item.

|        Shipping quote       |     |        POST/checkouts/{id}       |
| :-------------------------: | :-: | :------------------------------: |
|        `quotes[].id`        |  ➔  |   `shippingChoice.serviceLevel`  |
|       `quotes[].total`      |  ➔  |      `shippingChoice.amount`     |
| `quotes[].items[].shipFrom` |  ➔  | `shipFrom` or `items[].shipFrom` |
