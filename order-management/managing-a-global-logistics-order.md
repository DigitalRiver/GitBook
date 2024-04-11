---
description: Gain a better understanding of how to manage a Global Logistics order.
---

# Managing a Global Logistics order

On this page, you'll find an [overview of the order management process](managing-a-global-logistics-order.md#overview) in [Global Logistics](../using-our-services/global-logistics.md). For details about each stage, refer to:

* [Sending the ship request](managing-a-global-logistics-order.md#sending-the-ship-request)
* [Managing shipping labels](managing-a-global-logistics-order.md#managing-shipping-labels)
* [Tracking order shipments](managing-a-global-logistics-order.md#tracking-order-shipments)
* [Processing reversals](managing-a-global-logistics-order.md#processing-reversals)

## Overview

After the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md) moves to `accepted`, you must [send a ship request](managing-a-global-logistics-order.md#sending-the-ship-request) to your [third-party logistics](../general-resources/glossary.md#third-party-logistics) (3PL) provider so that the goods can be picked and packed at the appropriate warehouse. When ready to ship, your 3PL needs to [send a label request to Digital River](managing-a-global-logistics-order.md#defining-and-sending-the-shipping-label-request), which we route to the appropriate [global logistics provider (GLP)](../using-our-services/global-logistics.md#global-logistics-providers).

The GLP generates one or more shipping labels, sends those labels back to Digital River and we relay them to your 3PL.

The shipping label request also prompts the GLP to prepare an order's international shipping documentation. The GLP bundles this documentation in a pre-clearance request that gets sent to the destination country's customs agency.

Once the shipping labels are generated, a carrier retrieves the goods from the warehouse. In the [hub and spoke logistics model](../using-our-services/global-logistics.md#hub-and-spoke-logistics-model), the carrier delivers the products to a distribution hub before they are moved to an export gateway and then shipped to the end customer's address. In the [hubless model](../using-our-services/global-logistics.md#hubless-logistics-model), the carrier delivers the goods directly to an export gateway, where they are shipped to the final destination.

After the goods arrive in the destination country, the GLP ensures that they clear customs, moves them to a distribution site and coordinates with local carriers to deliver them the "final mile" to the end customer.

Once the shipping labels are generated, you can also use GL to [track an order's shipments](managing-a-global-logistics-order.md#tracking-order-shipments). For each shipment, we provide you information on its products and status, as well as events that occur at specific locations along a delivery's route.

## Sending the ship request

Once the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) moves to [`accepted`](creating-and-updating-an-order.md#handling-accepted-orders), you should use its data to send a ship request to your [3PL](../general-resources/glossary.md#third-party-logistics).

At a minimum, this request must include the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `id` as well as the `id` and `quantity` of each of the order's [physical](../product-management/skus.md#how-to-identify-a-physical-or-digital-sku) `items[]`.&#x20;

You'll also likely want to pass the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders):

* `shipFrom` so that your 3PL knows which warehouse to route the request to.
* `shipTo` so that your 3PL knows where the goods are going.
* The relevant `items[].productDetails` so that warehouse personnel know which products to pick and pack.

## **Managing shipping labels**

Once the goods are picked and packed, and a ship label needs to be printed, your 3PL needs to [define and send a shipping label request](managing-a-global-logistics-order.md#defining-and-sending-the-shipping-label-request) and then be setup to handle the [successful response](managing-a-global-logistics-order.md#the-shipping-label-response) as well as [potential errors](managing-a-global-logistics-order.md#failure-responses).&#x20;

If necessary, Global Logistics also provides the capability to [switch the fulfillment warehouse](managing-a-global-logistics-order.md#switching-the-fulfillment-warehouse).

### Defining and sending the shipping label request

In the [`POST /shipping-labels`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel) request, your [3PL](../general-resources/glossary.md#third-party-logistics) must send an [`orderId`](managing-a-global-logistics-order.md#order-identifier-1), a [`labelFormat`](managing-a-global-logistics-order.md#label-format), and [`items[]` nested in `packages[]`](managing-a-global-logistics-order.md#packaging-and-product-data).

Both [`shippingChoice` and `shipFrom`](managing-a-global-logistics-order.md#shipping-choice-and-ship-from) are optional.

#### Order identifier

When defining the request, retrieve the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `id` sent in the [ship request](managing-a-global-logistics-order.md#sending-the-ship-request) and use it to set `orderId`.

<table><thead><tr><th width="114">Order</th><th width="73" align="center"></th><th width="162">Ship request</th><th width="85" align="center"></th><th align="center">POST /shipping-labels</th></tr></thead><tbody><tr><td><code>id</code></td><td align="center"><strong>➔</strong></td><td>order identifier</td><td align="center"><strong>➔</strong></td><td align="center"><code>orderId</code></td></tr></tbody></table>

#### Shipping choice and ship from

The request's `shippingChoice` and `shipFrom` are optional because the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) already contains this data. If these parameters are not defined, then, by default, the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `shippingChoice` and `shipFrom` are encoded in the [shipping label's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels) data `file`.

For details, refer to [Switching the fulfillment warehouse](managing-a-global-logistics-order.md#switching-the-fulfillment-warehouse).

#### Packaging and product data

The request must contain `packages[]` and nested inside each element of this array must be one or more `items[]`.&#x20;

For each `packages[]`:

* The required `weight` should represent the scale weight of the package (with the goods and [dunnage](https://en.wikipedia.org/wiki/Dunnage) inside of it) at the warehouse. \
  \
  The enumerated `weightUnit` values are `oz`, `lb`, `g`, and `kg`.&#x20;
* The optional, but highly recommended `height`, `width`, and `length` should represent the actual dimensions of the package in inches.&#x20;

{% hint style="info" %}
It's important that a package's weight and dimensions be as accurate as possible. These values are used by carriers to determine a shipment's actual costs.&#x20;
{% endhint %}

For each `items[]` in that `packages[]` :

* The `itemId` is required. This represents the unique `id` of one of the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) physical `items[]`.

<table><thead><tr><th width="168">Order</th><th width="67" align="center"></th><th width="176">Ship request</th><th width="99" align="center"></th><th>POST /shipping-labels</th></tr></thead><tbody><tr><td><code>items[].id</code></td><td align="center"><strong>➔</strong></td><td>line item identifier</td><td align="center"><strong>➔</strong></td><td><code>items[].itemId</code></td></tr></tbody></table>

* The `quantity` is required.&#x20;

#### Label format

The `labelFormat` represents the file format you want the shipping labels to be returned in. You can ask for labels in `PDF`, `PNG`, `JPG`, `GIF`, or `ZPL`.&#x20;

### Switching the fulfillment warehouse

After the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is created, you might occasionally need to change its `shipFrom`. This typically happens when a [3PL](../general-resources/glossary.md#third-party-logistics) notifies you, after order submission, that the products are out-of-stock at the originally designated warehouse.

To handle this, first submit a [`POST /shipping-quotes`](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md#managing-shipping-quotes) and then, from the response, select a new `quotes[]`.

Next, [define a shipping label request](managing-a-global-logistics-order.md#defining-and-sending-the-shipping-label-request) by passing the selected `quotes[]` data in `shippingChoice` and `shipFrom`.&#x20;

{% hint style="danger" %}
If you don't use the `quotes[].id` to define `shippingChoice.id`, then the [create shipping label request](managing-a-global-logistics-order.md#managing-shipping-labels) will fail.
{% endhint %}

Once the request is successfully submitted, Digital River uses these values to update the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `shippingChoice` and `shipFrom`.

### How your request gets processed

When Global Logistics receives a [shipping label request](managing-a-global-logistics-order.md#defining-and-sending-the-shipping-label-request), we retrieve `orderId` from the payload and use it to look up the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in our system.&#x20;

We use `items[].id` to get data on the products going out in that shipment. This includes the product's name, declared value, tariff code, country of origin, and weight. If the product contains a part number, url, image, [signature requirements](../using-our-services/global-logistics.md#signature-requirements) and [dangerous goods classifications](../using-our-services/global-logistics.md#dangerous-goods-classifications), we pass that data as well.&#x20;

We then route a transformed request to the appropriate [GLP](../using-our-services/global-logistics.md#global-logistics-providers) who determines where the shipment is going and generates one or more labels that point the products to either the address of the end customer or the address of an in-country hub. The GLP also determines whether the products have any handling and/or signature requirements, and, if they do, adds them to the label's data.

A label request also prompts the GLP to prepare a shipment's customs documentation and then package it in a digital pre-clearance request that they typically send to an importation country's customs agency.

When the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) responds to our request for shipping labels, we log their reply and then pass a transformed response to your [3PL](../general-resources/glossary.md#third-party-logistics).

### Successful shipping label response <a href="#the-shipping-label-response" id="the-shipping-label-response"></a>

A successful response provides your [3PL](../general-resources/glossary.md#third-party-logistics) the data it needs to print one or more shipping labels. The response might also contain supplemental customs documentation.

{% hint style="info" %}
At this point, order tracking data typically becomes available. For details, refer to [Tracking order shipments](managing-a-global-logistics-order.md#tracking-order-shipments).
{% endhint %}

#### Unique identifier

The response contains a unique `id` whose value is generated by Digital River. You can pass this value as a query parameter in a [list shipping labels request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/listShippingLabel) or a path parameter in a [get unique shipping label request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/retrieveShippingLabels).&#x20;

#### Order identifier

The `orderId` identifies the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in Digital River's system. You can pass this value as a query parameter in a [list shipping labels request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/listShippingLabel).

#### Shipments

The response contains one or more `shipments[]`. Each shipment has a unique `id` plus one or more `labels[]` and `packages[]`.

Each shipping `labels[]` contains:

* A `height` and `width`. These are the label's dimensions. The values are denoted in inches.
* The `format` of the data `file`. The possible values are `PDF`, `PNG`,`JPG`, `GIF` or `ZPL`.

{% hint style="warning" %}
The value of `format` might not always be the same as the `labelFormat` specified in the request. This is because not all formats are supported by every [GLP](../using-our-services/global-logistics.md#global-logistics-providers). As a result, make sure your application first checks the value of `format` before attempting to print the label.&#x20;
{% endhint %}

* A `file` with binary base64 encoded data. In many cases, `file` only contains an encoded label. \
  \
  Sometimes however `file` also holds additional documentation, such as a [commercial invoice](https://en.wikipedia.org/wiki/Commercial\_invoice). This happens when the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) is unable to submit a digital pre-clearance request to a country's customs agency (not all country-carrier combinations support this feature).&#x20;

{% hint style="info" %}
In the [hub and spoke logistics model](../using-our-services/global-logistics.md#hub-and-spoke-logistics-model), each label's `file` encodes the address of one of the [GLP's](managing-a-global-logistics-order.md#global-logistics-providers) in-country hubs. In the [hubless logistics model](../using-our-services/global-logistics.md#hubless-logistics-model), this `file` encodes the end customer's ship to address.
{% endhint %}

* In some cases, there's a `fileUrl` that provides the web address of a decoded label.

Each `packages[]` in the response maps to one of the `packages[]` sent by the 3PL in the request.

#### **Return to address**

The `returnTo` contains the product return address assigned by the GLP. After a returns request is approved, you should instruct customers to mail the products they're sending back to this address.

The GLP always attempts to find a return to address that's in the same country (or at least the same political region) as the shipment's destination address. If no such location exists, then the return to address is the warehouse where the goods are picked and packed.

{% hint style="info" %}
The same `returnTo` is also contained in the [logistics return object](managing-a-global-logistics-order.md#the-logistics-returns-object).
{% endhint %}

You can use these `returnTo` values as you see fit. For example, you may decide to display them on a customer's order management page, include them in email notifications or list them on invoices.

### Failure responses

If you fail to define parameters marked as required in the [shipping label request specifications](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel), you'll receive an error. In addition, the following are other common reasons the request might fail:

* [Multiple package shipments are not supported by the carrier](managing-a-global-logistics-order.md#multi-package-shipments-not-supported)
* [Invalid `orderId`](managing-a-global-logistics-order.md#invalid-orderid)
* [Invalid `labelFormat`](managing-a-global-logistics-order.md#invalid-labelformat)
* [Invalid `items[].itemId`](managing-a-global-logistics-order.md#invalid-items-.itemid)
* [Invalid `shipFrom`](managing-a-global-logistics-order.md#invalid-shipfrom)

#### Multi-package shipments not supported

If the 3PL sends a `POST /shipping-labels` that contains multiple `packages[]`, and the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) that Global Logistics routes the request to determines that the shipment is assigned to a carrier that doesn't support multi-package shipments, then the GLP returns an error to GL. If you instructed a Digital River representative to deactivate the auto-split feature, GL passes this error back to the 3PL.&#x20;

To handle it, the 3PL could split the failed request into multiple `POST/ shipping-labels`, each with a single `packages[]`. Alternatively, 3PL personnel could repackage all the goods into a single, larger box and send one `POST /shipping-labels` with one `packages[]`.

{% code title="409 Conflict" %}
```json
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "request.shippingChoice.id",
            "message": "Multiple package shipments are not supported by the selected shipping choice."
        }
    ]
}
```
{% endcode %}

#### Invalid `orderId`

If the request contains an invalid `orderId`, then the following error is returned:

{% code title="404 Not Found" %}
```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "not_found",
            "parameter": "id",
            "message": "Order 'I8Na1N0gxyq8yni' not found."
        }
    ]
}
```
{% endcode %}

#### Invalid `labelFormat`

If the request contains an invalid `labelFormat`, then the following error is returned:

{% code title="409 Conflict" %}
```json
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_parameter",
            "message": "The label format is invalid."
        }
    ]
}
```
{% endcode %}

#### Invalid `items[].itemId`

If the request contains an invalid `packages[].items[].itemId`, then the following error is returned:

{% code title="400 Bad Request" %}
```
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "message": "The original order items is required."
        }
    ]
}
```
{% endcode %}

#### Invalid `shipFrom`

If the request contains a `shipFrom` that's not supported by your [trading patterns](../using-our-services/global-logistics.md#defining-trading-patterns), then the following error is returned:

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "message": "The logistics partner was not found."
        }
    ]
}
```
{% endcode %}

#### Invalid `weightUnit`

If the request contains a `weightUnit` that's not an enumerated value, then the following error is returned:

{% code title="400 Bad Request" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "packages[0].weightUnit",
            "message": "'lbs' is not a valid item type."
        }
    ]
}
```
{% endcode %}

### Handling the shipping label response

For each `shipments[]`, the 3PL needs to iterate through each `labels[]`, decode its base64 data [`file`](managing-a-global-logistics-order.md#the-shipping-label-response), and then write the binary out to the designated `format`.&#x20;

The 3PL can then open the file, configure the label's dimensions using `height` and `width`, print the label and affix it to one of the shipment's `packages[]`.

{% hint style="info" %}
If a `shipments[]` contains multiple `labels[]`, then it doesn't matter which gets affixed to each `packages[]`. A label's `file` doesn't contain any product data which means that no one-to-one association exists between a shipment label and a shipment package.&#x20;
{% endhint %}

When a  `labels[].file` contains additional documentation, such as the commercial invoice, the [3PL](../general-resources/glossary.md#third-party-logistics) must also print this paperwork and secure it to that shipment's `packages[]`.

{% tabs %}
{% tab title="Shipping label" %}
![](<../.gitbook/assets/shipping label erased.png>)
{% endtab %}

{% tab title="Customs documentation" %}
![](<../.gitbook/assets/commercial invoice erased.png>)
{% endtab %}
{% endtabs %}

Alternatively, if `labels[]` contains a `fileUrl`, the [3PL](../general-resources/glossary.md#third-party-logistics) can access the label resource at that address, print it and affix it to a `packages[]`.

Once the goods ship, your 3PL typically sends a notification to your system that triggers a [payment capture request](informing-digital-river-of-a-fulfillment.md).

### How the goods move to the end customer

In the [hub and spoke logistics model](../using-our-services/global-logistics.md#hub-and-spoke-logistics-model), the [3PL](../general-resources/glossary.md#third-party-logistics) affixed shipping labels direct the goods to a [GLP](../using-our-services/global-logistics.md#global-logistics-providers) hub. At this hub, the final destination shipping labels are printed and put on the packages. The GLP then moves the goods to an export gateway before shipping them to the destination country.

In the [hubless model](../using-our-services/global-logistics.md#hubless-logistics-model), the [3PL](../general-resources/glossary.md#third-party-logistics) affixed shipping labels direct the goods to one of the GLP's export gateways. At this facility, the final destination shipping labels are printed and attached and then the goods are shipped.

{% hint style="info" %}
If customers selected a quote with DAP [shipping terms](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md#shipping-terms) during the checkout process, then the recipient is required to pay the unpaid balance at the time of delivery. On the other hand, in shipments whose terms are DDP, the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) pays the duties, fees, and import taxes assessed by a country's custom agency.
{% endhint %}

Once the goods clear customs, the GLP coordinates with local carriers to move the products to a distribution warehouse where they are retrieved and delivered the "final mile" to the order's ship to address.

## Tracking order shipments

In this section, you'll find details on:

* [Sending the order tracking request](managing-a-global-logistics-order.md#sending-the-order-tracking-request)
* [When tracking information becomes available](managing-a-global-logistics-order.md#when-tracking-information-becomes-available)
* [The order tracking response](managing-a-global-logistics-order.md#the-order-tracking-response)
* [Handling the order tracking response](managing-a-global-logistics-order.md#handling-the-order-tracking-response)

### Sending the order tracking request

To track shipments, send an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) unique identifier as a path parameter in a `GET  /orders/{id}/tracking`.&#x20;

{% code title="GET /orders/{id}/tracking" %}
```javascript
curl --location --request GET 'https: //api.digitalriver.com/orders/1003597810082/tracking' \
...
```
{% endcode %}

This request is most commonly initiated when customers go to their order management page and select a specific order they want to track.

### When tracking information becomes available

Order tracking information typically becomes available after the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) generates a [shipping label](managing-a-global-logistics-order.md#the-shipping-label-response) and creates a shipment. If you send a `GET /orders/{id}/tracking` request prior to label generation, then the following error is thrown:

{% code title="404 Not Found" %}
```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "orderId",
            "message": "There are no shipments found for an order."
        }
    ]
}
```
{% endcode %}

Less commonly, the GLP creates a shipping label, but, for whatever reason, has yet to generate a shipment's tracking information. In this case, a `GET /orders/{id}/tracking` request returns the following error:

{% code title="404 Not Found" %}
```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "orderId",
            "message": "The tracking information was not found for an order or order has not been shipped yet."
        }
    ]
}
```
{% endcode %}

### The order tracking response

In the order tracking response, you'll find real-time data on the `items[]` in each `shipments[]` as well as their `shipFrom` location and delivery `status`.

{% code title="Order tracking" %}
```javascript
{
    "orderId": "1003597810082",
    "shipTo": {
        "address": {
            "line1": "10-123 1/2 MAIN STREET NW",
            "city": "MONTREAL",
            "postalCode": "H3Z 2Y7",
            "country": "CA"
        },
        "name": "JOHN JONES",
        "phone": "367-222-4321",
        "email": "jchou@digitalriver.com",
        "organization": "Digital River"
    },
    "shipments": [
        {
            "id": "100000048501",
            "status": "pending_shipment",
            "shipFrom": {
                "address": {
                    "city": "Salt Lake City",
                    "postalCode": "84604",
                    "state": "Utah",
                    "country": "US"
                }
            },
            "items": [
                {
                    "itemId": "11668110082",
                    "productDetails": {
                        "name": "PhysicalSku_1639749025",
                        "skuGroupId": "group_1639749011",
                        "weight": 0.0,
                        "weightUnit": "lb",
                        "countryOfOrigin": "US"
                    },
                    "quantity": 1
                }
            ],
            "trackingDetails": [
                {
                    "date": "2021-12-20T02:46:43",
                    "description": "Order Data Created/Received",
                    "location": "-"
                },
                {
                    "date": "2021-12-19T19:47:16",
                    "description": "Shipping Label Generated",
                    "location": "Salt Lake City Utah US"
                }
            ]
        }
    ],
    "liveMode": false
}
```
{% endcode %}

#### **Order identifier**

The response contains a single `orderId` that identifies the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in Digital River's system.

#### Ship to

In `shipTo`, you're given the final delivery `address` of the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) products, along with details on the buyer.&#x20;

#### Shipments

Each `shipments[]` represents a unique shipment. We return an array because an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) goods are sometimes sent out for delivery in multiple batches.

Each element in `shipments[]` contains:

* A unique `id` generated by Digital River.
* A `shipFrom` that represents the address of the warehouse where the products were picked and packed.
* One or more `items[]`, each that have an `itemId` generated by Digital River, plus [`productDetails`](../product-management/using-product-details.md) and a shipped `quantity`.&#x20;
* An overall `status` of that particular shipment.

{% hint style="info" %}
Each [GLP](../using-our-services/global-logistics.md#global-logistics-providers) maintains its own unique shipment statuses that Digital River normalizes to one of our `status` values .&#x20;
{% endhint %}

* Various `trackingDetails[]` that provide you a `description` and `status` of an event that occurred at a particular `location` on a specific `date`.  The [date-time values](../developer-resources/api-structure.md#dates-and-times) are the local time at the specified `location`.&#x20;

| array index | date                   | location                     | description                                           |
| ----------- | ---------------------- | ---------------------------- | ----------------------------------------------------- |
| 0           | `2021-08-13T15:20:00Z` | `-`                          | `Order Data Created/Received`                         |
| 1           | `2021-08-13T15:21:00Z` | `Salt Lake City Utah US`     | `Shipping Label Generated`                            |
| 2           | `2021-08-13T20:36:00Z` | `Salt Lake City Utah US`     | `Customs status updated`                              |
| 3           | `2021-08-16T08:15:00Z` | `LOS ANGELES GATEWAY,CA-USA` | `Arrived at Sort Facility LOS ANGELES GATEWAY,CA-USA` |
| 4           | `2021-08-19T03:32:00Z` | `BRUSSELS-BEL`               | `Transferred through BRUSSELS-BEL`                    |
| 5           | `2021-08-20T14:06:00Z` | `POINTE NOIRE-COG`           | `Clearance processing complete at POINTE NOIRE-COG`   |

### Handling the order tracking response

For each [`shipments[]`](managing-a-global-logistics-order.md#shipments), you can use its `items[]` to display product details, `status` to inform customers about a shipment's overall progress, and `trackingDetails[]` to give them a `description` and `status` of an event that occurred at a particular `location` on a specific `date`.

As with all [dates and times in the Digital River APIs](../developer-resources/api-structure.md#dates-and-times), we recommend you transform `date` in `trackingDetails[]` into a more human-readable form before you display it to customers.

![](<../.gitbook/assets/Shipment tracking.png>)

## Processing reversals

The Global Logistics (GL) solution allows you to process [customer-initiated returns](managing-a-global-logistics-order.md#customer-initiated-returns), [delivery refusals](managing-a-global-logistics-order.md#delivery-refusals), and [undeliverable packages](managing-a-global-logistics-order.md#undeliverable-packages). You do this by sending return requests and/or listening for return events.

When you receive a [`logistics-returns.received`](managing-a-global-logistics-order.md#the-logistics-returns-object) event, use its [`type`](managing-a-global-logistics-order.md#type) to appropriately update the status of the return in your system and notify customers of the accepted return, refused delivery, or undeliverable package.

At any stage of the returns process, you can give customers a refund by using the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds). For details, refer to the [Issuing refunds](returns-and-refunds-1/refunds/issuing-refunds.md) page.

### Customer-initiated returns

The following describes how to process customer-initiated returns that stem from damaged goods, faulty products, a 'change-of-heart' and other similar scenarios.

#### Defining and sending a logistics returns request

If a customer requests a return, and you determine the request is valid, your order management system needs to define and send a [`POST /logistics-returns`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Logistics-Returns/operation/createLogisticsReturns). You can configure this request to generate both full and partial order returns.

{% code title="POST/logistics-returns" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/logistics-returns' \
...
--data-raw '{
    "orderId": "1006970340082",
    "rmaNumber": "57d34656-966e-4bcf-ad87-4c44ae1beb14",
    "reason": "Damaged",
    "items": [
        {
            "itemId": "10366350082",
            "quantity": 3
        }
    ]
}'
```
{% endcode %}

The request must include `orderId`. This value identifies the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in Digital River's system.

For each product being returned, you also need to send an `items[].itemId` that identifies the[ `items[]`](creating-and-updating-an-order.md#line-items) in the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), plus the `quantity` being returned.

Additionally, you're required to pass the [return merchandise authorization](https://en.wikipedia.org/wiki/Return\_merchandise\_authorization) number generated by your system in `rmaNumber`.

If you send `reason`, neither Digital River or the [global logistics provider](../using-our-services/global-logistics.md#global-logistics-providers) (GLP) use this value. But depending on how you build your integration, you may find it useful for customer service or record-keeping purposes.

#### How your request is handled

Digital River uses `orderId` and `items[].itemId` to look up the relevant shipment and product details and then routes your return authorization request to the appropriate [GLP](managing-a-global-logistics-order.md#global-logistics-providers). Upon receipt of this request, the GLP marks the return as pending, acknowledges the request and waits for the specified goods to arrive at their facility.

#### The logistics return response

The body of a successful [`POST /logistics-returns`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns/operation/createReturns) response contains a [logistics return object](managing-a-global-logistics-order.md#the-logistics-returns-object) whose [`type`](managing-a-global-logistics-order.md#type) is `authorization`. This indicates the [GLP](../using-our-services/global-logistics.md#global-logistics-providers) has received your return authorization request.

{% code title="Logistics return" %}
```javascript
{
    "id": "100000032201",
    "createdTime": "2022-01-10T16:56:22Z",
    "orderId": "1006970340082",
    "rmaNumber": "e0e09e8e-9363-46ff-9baa-2485316e8b07",
    "reason": "Damaged",
    "type": "authorization",
    "items": [
        {
            "itemId": "10366350082",
            "quantity": 3,
            "productDetails": {
                "partNumber": "PN_physku1_1641832892693",
                "name": "Physical SKU, fulfilled by DR",
                "skuGroupId": "16f794d0-6143-45ed-8f14-c933f0983e7b",
                "weight": 3.0,
                "weightUnit": "oz",
                "countryOfOrigin": "AU"
            }
        }
    ],
    "returnTo": {
        "address": {
            "line1": "123 Airport Road",
            "city": "Salt Lake City",
            "postalCode": "84604",
            "state": "Utah",
            "country": "US"
        },
        "phone": "555-555-5555",
        "organization": "DR Client 4",
        "additionalAddressInfo": {}
    },
    "liveMode": false
}
```
{% endcode %}

#### Handling the logistics return response

Upon receiving a `201 Created` status code, provide customers with the [`orderId`](managing-a-global-logistics-order.md#order-identifier-3) and [`rmaNumber`](managing-a-global-logistics-order.md#rma-number) and tell them to either write these identifiers directly on the returns package or include them on the shipping documentation inside the package.

Make sure you provide customers the full [`returnTo`](managing-a-global-logistics-order.md#return-to) and instruct them to mail the products to that address.

{% hint style="warning" %}
Customers are responsible for shipping the goods to the designated address. The GL solution currently doesn't support return ship label generation, supplying customers with pre-paid return ship labels, or carrier pickups from the customer's address.
{% endhint %}

#### Handling the return received event

When the goods arrive at the [GLP's](../using-our-services/global-logistics.md#global-logistics-providers) facility, their personnel use the included order identifier and RMA number to look up the pending return in their system. Their staff then inspect the products to verify their quality and quantity match the information in the returns authorization request.

{% hint style="info" %}
If the returned goods don't arrive in the expected condition or their quantity is less than anticipated, the GLP, using a pre-arranged process, will contact your customer service team.
{% endhint %}

At this point, the GLP (1) sends an API call to Digital River that indicates the goods have been received and accepted and (2) processes the returned goods according to your [disposition agreement](../using-our-services/global-logistics.md#set-up-a-product-disposition-agreement).

Upon receiving this API call, Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is [`logistics-return.received`](managing-a-global-logistics-order.md#the-logistics-returns-object) and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) contains a [`type`](managing-a-global-logistics-order.md#type) of `received`.

Depending on your return and refund policies, as well as how you structure your workflow, you may decide to use this event to trigger a [`POST /refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) request.

### Delivery refusals

If a carrier attempts to deliver a package, but the recipient refuses delivery, then the goods are returned to a [GLP](../using-our-services/global-logistics.md#global-logistics-providers) facility within the destination country.

{% hint style="info" %}
Customers sometimes refuse a delivery because they aren't expecting any packages. Alternatively, when a shipment's duty payment terms are delivered-at-place, customers may be unaware of the outstanding duties, fees, and import taxes.
{% endhint %}

At this point, the GLP (1) sends an API call to Digital River that indicates the goods have been refused by the customer and (2) processes the refused goods according to your [disposition agreement](../using-our-services/global-logistics.md#set-up-a-product-disposition-agreement).

Upon receiving this API call, Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is [`logistics-return.received`](managing-a-global-logistics-order.md#the-logistics-returns-object) and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) contains a [`type`](managing-a-global-logistics-order.md#type) of `refused`. This event should trigger a [`POST /refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) request.

### Undeliverable packages

Sometimes packages are undeliverable. This is often due to an incorrect ship to address (e.g., the house or apartment number is inaccurate) on the shipping label. Less commonly, it's because the customer isn't present to sign for delivery or the designated address is a restricted institution (e.g., a prison or correctional facility) that requires advanced permission to enter.

In these scenarios, the carrier typically makes multiple delivery attempts. Additionally, the GLP supplies your customer service team with undelivered shipments reports which they can use to contact customers and attempt to correct the invalid address or obtain an alternative address.

However, if their attempts prove unsuccessful, inform the GLP so that the goods can be returned to their facility within the destination country. At that point, the GLP (1) sends an API call to Digital River that indicates the goods are undeliverable and (2) processes them according to your [disposition agreement](managing-a-global-logistics-order.md#set-up-a-product-disposition-agreement).

Upon receiving this API call, Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is [`logistics-return.received`](managing-a-global-logistics-order.md#the-logistics-returns-object) and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) contains a [`type`](managing-a-global-logistics-order.md#type) of `undeliverable`. This event should trigger a [`POST /refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) request.

### The logistics returns object

The response body of a [`POST /logistics-return`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Logistics-Returns) and the [`data.object`](events-and-webhooks-1/events-1/#event-data) of the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is `logistics-return.received` share the same schema. The following is some of the key data in this object:

* [Unique identifier](managing-a-global-logistics-order.md#logistics-return-identifier)
* [Order identifier](managing-a-global-logistics-order.md#order-identifier-3)
* [RMA number](managing-a-global-logistics-order.md#rma-number)
* [Product information](managing-a-global-logistics-order.md#product-information)
* [Reason for return](managing-a-global-logistics-order.md#reason)
* [The type of return](managing-a-global-logistics-order.md#type)
* [The return address](managing-a-global-logistics-order.md#return-to)

For a complete schema definition, refer to [logistics returns](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Logistics-Returns) on the [Digital River API reference](https://www.digitalriver.com/docs/digital-river-api-reference/) site.

#### Logistics return identifier

The `id` uniquely identifies the logistics return. You can send this value as a path parameter in a [`GET /logistics-returns/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Logistics-Returns/operation/retrieveLogisticsReturns) and as a query parameter in a [`GET /logistics-returns`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Logistics-Returns/operation/listLogisticsReturns) request.

#### Order identifier

The `orderId` references the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in Digital River's system.

#### RMA number

The `rmaNumber` represents the [return merchandise authorization](https://en.wikipedia.org/wiki/Return\_merchandise\_authorization) number generated by your order management system. This field is only populated in [customer-initiated returns](managing-a-global-logistics-order.md#customer-initiated-returns).

#### Product information

Each `itemId` references an [`items[]`](../developer-resources/digital-river-api-reference/orders/#line-items) in the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in Digital River's system. We also provide the [`productDetails`](../product-management/using-product-details.md) associated with that line item.

Additionally, when the goods arrive back at the GLP's facility, their personnel inspect them and record their `condition`.

#### Reason

The `reason` is collected from the customer during the return validation process. This field is only populated in [customer-initiated returns](managing-a-global-logistics-order.md#customer-initiated-returns).

#### Type

You can use `type` to determine both the category and status of a logistics return:

* `authorization`: In [customer-initiated returns](managing-a-global-logistics-order.md#customer-initiated-returns), this value indicates the [GLP](managing-a-global-logistics-order.md#global-logistics-providers) has acknowledged your `POST /logistics-returns` request and is awaiting the returned goods.
* `received`: In [customer-initiated returns](managing-a-global-logistics-order.md#customer-initiated-returns), this value indicates that the goods have arrived at the GLP's facility and their personnel have inspected and approved the return.
* `undeliverable`: In [undeliverable return scenarios](managing-a-global-logistics-order.md#undeliverable-packages), this value indicates that, after repeated attempts, the carrier was unable to make delivery and the GLP has marked the shipment as undeliverable.
* `refused`: In [refusal return scenarios](managing-a-global-logistics-order.md#delivery-refusals), this value indicates that the customer has rejected delivery of the goods and the GLP marked the shipment as refused.

Once `type` is `received`, `undeliverable`, or `refused`, the GLP processes the returned goods according to your [disposition agreement](../using-our-services/global-logistics.md#set-up-a-product-disposition-agreement)

#### Return to

In a logistics return object, `returnTo` contains the address where end customers must mail products. This is the same `returnTo` in the [shipping label response](managing-a-global-logistics-order.md#the-shipping-label-response).
