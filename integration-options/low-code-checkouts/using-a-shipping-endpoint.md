---
description: >-
  Gain a better understanding of how you can use a shipping endpoint to present
  dynamic shipping options in low-code checkouts
---

# Using a shipping endpoint

With [low-code checkouts](./), you have the option of saving a [shipping endpoint in Digital River Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#configure-a-shipping-callout). Digital River calls it during checkouts that involve [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) and uses the response to present customers with their shipping options.&#x20;

Depending on whether you're using [Global Logistics](../../using-our-services/global-logistics.md) and/or an external logistics provider, the service you set up to handle our call can either filter and adjust the shipping options we send or use the request's data to make another request to your external provider to get the available options from them.&#x20;

In both cases, you must respond with the options you want us to present to customers in the shipping choice selection stage. &#x20;

On this page, you’ll find details on:

* [Creating the checkout-session](using-a-shipping-endpoint.md#creating-the-checkout-session)
* [Restricting available ship to countries](using-a-shipping-endpoint.md#restricting-available-ship-to-countries)
* [How to use the endpoint with Global Logistics](using-a-shipping-endpoint.md#using-the-endpoint-with-global-logistics)
* [How to use the endpoint with an external logistics provider](using-a-shipping-endpoint.md#using-the-endpoint-with-an-external-logistics-providers)
* [How to display error messages](using-a-shipping-endpoint.md#displaying-errors)

## Creating the checkout-session

In your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), include the `weight` and `weightUnit` of each [physical product](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) in the cart in either the [SKU](../../product-management/creating-and-updating-skus.md) referenced by `items[].skuId` or directly in [`items[].productDetails`](../../product-management/using-product-details.md).&#x20;

{% hint style="info" %}
A product's weight should be exclusive of its packaging but inclusive of its [dunnage](https://en.wikipedia.org/wiki/Dunnage). In other words, don't include the weight of the product's box but do include the weight of the protective and supporting materials that go inside of it.
{% endhint %}

[Global Logistics](../../using-our-services/global-logistics.md) uses this data to get more precise shipping rates, and, if the transaction is being facilitated by an external logistics provider, it's likely they can do the same.

Goods eligible for inclusion in [cross-border shipments](../../general-resources/glossary.md#cross-border) should also be assigned a `name`, `description`, `image`, and `url`. For details on why this is important, refer to [Defining basic product data](../../using-our-services/global-logistics.md#defining-basic-product-data) on the [Global Logistics](../../using-our-services/global-logistics.md) page.&#x20;

## Restricting available ship to countries

You'll need to restrict the countries that customers can select from during the shipping address collection stage to those that you support.&#x20;

For details on how to do this, refer to [Shopping country](../../developer-resources/digital-river-api-reference/checkout-sessions.md#shopping-country) on the [Checkout-sessions](../../developer-resources/digital-river-api-reference/checkout-sessions.md) page.&#x20;

{% hint style="info" %}
In [Prebuilt Checkout](drop-in-checkout.md), you can also use its [configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/) to [restrict shipping and billing countries](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#restrict-shipping-and-billing-countries).
{% endhint %}

## Using the endpoint with Global Logistics

If you (1) select either [low-code checkout](./) solution, (2) enable the [Global Logistics](../../using-our-services/global-logistics.md) service, and (3) [save a shipping endpoint in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#configure-a-shipping-callout), then you can use this section to better understand:&#x20;

* [The shipping quotes request we send to your endpoint](using-a-shipping-endpoint.md#the-shipping-quotes-request)
* [How to process and respond to our request](using-a-shipping-endpoint.md#processing-and-responding-to-our-request)
* [How Digital River processes your response](using-a-shipping-endpoint.md#how-digital-river-processes-your-response)
* [How the ship request can be defined](using-a-shipping-endpoint.md#defining-the-ship-request)

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Shipping endpoint with GL (7).png" alt=""><figcaption></figcaption></figure>

</div>

### The shipping quotes request

Once customers input a shipping address, and it's determined that the transaction matches one of your [trading patterns](../../using-our-services/global-logistics.md#defining-trading-patterns), our [Global Logistics](../../using-our-services/global-logistics.md) service calls the appropriate [Global Logistics Provider](../../using-our-services/global-logistics.md#global-logistics-providers) to get the available shipping options.&#x20;

{% hint style="info" %}
In that same request, Global Logistics also passes any [default package data](../../using-our-services/global-logistics.md#default-box) saved to your account.
{% endhint %}

We then send a request to [your shipping endpoint](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Shipping-Quotes/operation/listShippingMethodQuotes). The body of that request:

* Lists these available options in `shippingMethods[]`, each element of which has an `amount`, `description`, `serviceLevel`, `shippingTerms`, `shipFrom`, and a unique `id` and may contain an `estimatedDelivery`.
* Contains the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `currency`, `shipTo`, `items[]`, and unique identifier (`sessionId`). &#x20;

{% code title="Request" %}
```json
{
    "sessionId": "614fa310-2e62-442f-8499-4a3d2b55fef4",
    "currency": "EUR",
    "shipTo": {
        "address": {
            "line1": "Oranienburger Str. 32",
            "city": "Berlin",
            "postalCode": "10117",
            "country": "DE"
        },
        "name": "Johann Doe",
        "phone": "07854319925",
        "email": "jdoe@digitalriver.com"
    },
    "items": [
        {
            "sku": {
                "id": "sku_e628c0d0-33b7-4dea-aa40-9eadc43e1583",
                "name": "Red shirt",
                "eccn": "8A992",
                "taxCode": "55101504.100",
                "image": "https://mdbootstrap.com/img/Photos/Horizontal/E-commerce/Vertical/12.jpg",
                "url": "https://digitalriver.com/physical-product",
                "physical": true,
                "skuGroupId": "physical-product",
                "weight": 20.5,
                "weightUnit": "oz"
            },
            "amount": 11.95,
            "quantity": 1,
            "id": "948264e5-13ac-4001-b553-baea65cdcdea"
        }
    ],
    "shippingMethods": [
        {
            "id": "07",
            "amount": 15.06,
            "description": "Economy",
            "serviceLevel": "XLTUS-DEFAULT",
            "shippingTerms": "DAP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        },
        {
            "id": "23",
            "amount": 17.17,
            "description": "Express",
            "serviceLevel": "XLTUS-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        },
        {
            "id": "57",
            "amount": 18.1,
            "description": "Economy",
            "serviceLevel": "XLTUK-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        },
        {
            "id": "68",
            "amount": 24.84,
            "description": "Express",
            "serviceLevel": "XLTUK-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        }
    ]
}
```
{% endcode %}

### Processing and responding to our request

Your service could process these available `shippingMethods[]` by:

* Discarding all the elements that have [`shippingTerms`](../checkouts/interacting-with-global-logistics-in-checkouts.md#shipping-terms) of `DAP` in an effort reduce the frequency of delivery refusals and returns.
* Reducing one or more `amount` values to give your customers a discount on their shipping costs.

In your response, use `shippingMethods[]` to list the options you want Digital River to display to customers. The attributes of each element in this array must map to a shipping option we sent in the request, and, other than `amount`, should pass back the same values.

* `id`, `description`, `serviceLevel`, `shippingTerms` , `shipFrom` , and `amount` are all required

{% hint style="danger" %}
If you fail to return `id`, the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) can be successfully created, but the [create shipping label request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel) will fail.&#x20;
{% endhint %}

* `estimatedDelivery` is optional

{% code title="Response" %}
```json
{
    "shippingMethods": [
        {
            "id": "23",
            "amount": 16.99,
            "description": "Express",
            "serviceLevel": "XLTUS-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        },
        {
            "id": "57",
            "amount": 17.99,
            "description": "Economy",
            "serviceLevel": "XLTUK-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        },
        {
            "id": "68",
            "description": "Express",
            "serviceLevel": "XLTUK-DEFAULT",
            "shippingTerms": "DDP",
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            }
        }
    ]
}
```
{% endcode %}

### How Digital River processes your response

For each `shippingMethods[]` in your response, Digital River displays its `amount`, `description`, [`shippingTerms`](../../general-resources/glossary.md#shipping-terms) , and (if it exists) `estimatedDelivery` in the shipping choice selection stage.

{% hint style="info" %}
In [Prebuilt Checkout](drop-in-checkout.md), Digital River renders [`shippingTerms`](../../general-resources/glossary.md#shipping-terms) in such a way that its meaning is clearer to customers. [Components](using-a-shipping-endpoint.md#components) does not yet display `estimatedDelivery` or `shippingTerms`.
{% endhint %}

Each time customers make a selection, we use its data to update the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shippingChoice` and [`shipFrom`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#ship-from).

### Defining the ship request

After Digital River converts the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and sends you the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`order.accepted`](../../order-management/events-and-webhooks-1/events-1/event-types.md#order.accepted), you can retrieve `shippingChoice` and `shipFrom`  from its [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) and then pass it (along with other required data) in a ship request to your 3PL so that they have the necessary data to send to [Global Logistics](../../using-our-services/global-logistics.md) in a [`POST /shipping-labels`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels/operation/createShippingLabel) request.\
\
For details, refer to [Managing a Global Logistics order](../../order-management/managing-a-global-logistics-order.md).

{% code title="Event" %}
```json
{
    "id": "e7f66af3-4207-4c23-b866-73efc8449525",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "255895420336",
           ...
            "shipFrom": {
                "address": {
                    "city": "Los Angeles",
                    "postalCode": "90245",
                    "state": "California",
                    "country": "US"
                }
            },
            ...
            "shippingChoice": {
                "amount": 17.99,
                "description": "Economy",
                "serviceLevel": "XLTUS-DEFAULT",
                "taxAmount": 0.0,
                "shippingTerms": "DDP"
            },
            ...
            "state": "accepted",
            ...
        }
    },
    ...
}
```
{% endcode %}

## Using the endpoint with an external logistics providers

If you (1) select either [low-code checkout](./) solution, (2) [save a shipping endpoint in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#configure-a-shipping-callout) and (3) engage an external logistics service, you can use this section to better understand:

* [The shipping quotes request we send to your endpoint](using-a-shipping-endpoint.md#the-shipping-quotes-request-1)
* [How to process and respond to our request](using-a-shipping-endpoint.md#processing-and-responding-to-our-request-1)
* [How Digital River processes your response](using-a-shipping-endpoint.md#how-digital-river-processes-your-response-1)
* [How the ship request can be defined](using-a-shipping-endpoint.md#defining-the-ship-request-1)



<div data-full-width="true">

<figure><img src="../../.gitbook/assets/Shipping endpoint 3rd party (2).png" alt=""><figcaption></figcaption></figure>

</div>

### The shipping quotes request

Once customers input a shipping address and Digital River determines that an external logistics provider is facilitating the transaction, we send a request to [your shipping endpoint](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Shipping-Quotes/operation/listShippingMethodQuotes).

{% code title="Request" %}
```json
{
    "sessionId": "8e8f8a1b-4049-4e4f-a8b6-d5c6a90b713b",
    "currency": "USD",
    "shipTo": {
        "address": {
            "line1": "1234 Rocky Mountain Highway",
            "city": "Estes Park",
            "state": "CO",
            "postalCode": "80517",
            "country": "US"
        },
        "name": "John D.",
        "phone": "5555555555",
        "email": "jdenver@digitalriver.com"
    },
    "items": [
        {
            "sku": {
                "id": "sku_e628c0d0-33b7-4dea-aa40-9eadc43e1583",
                "name": "Blue shirt",
                "eccn": "8A992",
                "taxCode": "55101504.100",
                "image": "https://mdbootstrap.com/img/Photos/Horizontal/E-commerce/Vertical/12.jpg",
                "url": "https://digitalriver.com/blue-shirt",
                "physical": true,
                "skuGroupId": "physical-product",
                "weight": 20.5,
                "weightUnit": "oz"
            },
            "amount": 11.95,
            "quantity": 1,
            "id": "714eb8ef-5a11-4faa-b6e5-35992d01d628"
        },
        {
            "sku": {
                "id": "sku_32ee813a-e7a8-46dc-97f4-fca07b47eca6",
                "name": "Red shirt",
                "eccn": "8A992",
                "taxCode": "55101504.100",
                "image": "https://mdbootstrap.com/img/Photos/Horizontal/E-commerce/Vertical/12.jpg",
                "url": "https://digitalriver.com/red-shirt",
                "physical": true,
                "skuGroupId": "physical-product",
                "weight": 20.5,
                "weightUnit": "oz"
            },
            "amount": 11.95,
            "quantity": 1,
            "id": "945gh8ed-3g21-6ffg-mj6e6-45113e11d628"
        }
    ]
}
```
{% endcode %}

Since we don't yet know what shipping options are available, the request contains no `shippingMethods[]`.&#x20;

It does, however, contain the [checkout-session’s](../../developer-resources/digital-river-api-reference/checkout-sessions.md) `currency`, `shipTo`, `items[]`, and unique identifier (`sessionId`).&#x20;

For each `items[]`, we also give you an `id` that uniquely identifies that line item in our system.

### Processing and responding to our request

After you accept our request and determine that it contains no `shippingMethods[]`, you can use its `currency`, `items[]`, and `shipTo` to call your logistics provider and get the transaction’s available shipping options.&#x20;

In that request, you'll most likely want to pass the `weight` and `weightUnit` of each `items[]`. Your logistics provider can typically use that data to give you back more precise shipping rates.

In addition, depending on the sophistication of the integration you have with your provider, they might be able to give you the location of the warehouse(s) from which each `items[]` will be shipped.&#x20;

After your logistics provider returns the available shipping options, your service could add a markup, discount them, and/or filter them by terms.&#x20;

Your response must contain `shippingMethods[]`, which contain the options you want Digital River to present in the shipping choice selection stage. Each element in this array must have an `amount`, `description`, and `serviceLevel` and can optionally include an `id`, `estimatedDelivery`, `shippingTerms`, and a `shipFrom` location.

If your logistic provider informed you where each line item is shipping from, your response can also contain `shipments[]`, each of which should have a single `shipFrom` and an array of `itemIds[]`, each mapped to an `items[].id` we sent in the request.&#x20;

{% code title="Response" %}
```json
{
    "shipments": [
        {
            "itemIds": [
                "714eb8ef-5a11-4faa-b6e5-35992d01d628"
            ],
            "shipFrom": {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "state": "MN",
                    "country": "US"
                }
            }
        },
        {
            "itemIds": [
                "945gh8ed-3g21-6ffg-mj6e6-45113e11d628"
            ],
            "shipFrom": {
                "address": {
                    "line1": "1234 5th Ave",
                    "city": "New York",
                    "postalCode": "10005",
                    "state": "NY",
                    "country": "US"
                }
            }
        }
    ],
    "shippingMethods": [
        {
            "description": "Standard Shipping",
            "serviceLevel": "Standard",
            "amount": 2.99
        },
        {
            "description": "Expedited Shipping",
            "serviceLevel": "Expedited",
            "amount": 10.98
        }
    ]
}
```
{% endcode %}

### How Digital River processes your response

For each `shipments[]` in your response, we iterate through its `itemsIds[]`, looking up that resource in our system and then use the `shipments[].shipFrom` to set the appropriate `items[].shipFrom` value(s) in the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions).&#x20;

For each `shippingMethods[]`, Digital River displays its `amount`, `description`, `shippingTerms`, and `estimatedDelivery` to customers in the shipping choice selection stage.

{% hint style="info" %}
In [Prebuilt Checkout](drop-in-checkout.md), Digital River renders [`shippingTerms`](../../general-resources/glossary.md#shipping-terms) in such a way that its meaning is clearer to customers. [Components](using-a-shipping-endpoint.md#components) does not yet display `estimatedDelivery` or `shippingTerms`.
{% endhint %}

Each time customers make a selection, we use its data to update the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shippingChoice` and, if that selection contains a `shipFrom` , we also use it to set that resource's [`shipFrom`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#ship-from).

### Defining the ship request

After Digital River converts the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and sends you the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`order.accepted`](../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event), you can pass its data to your fulfillment service, which can then read the line-item level and/or order-level ship from values and route ship requests to the appropriate warehouses.

{% code title="Event" %}
```json
{
    "id": "a443e1ee-61ec-4f9c-8c27-97b144c8f8f5",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "255896870336",
            ...
            "items": [
                {
                    "id": "185466030336",
                    "productDetails": {
                        "id": "physical-product-1",
                        "skuGroupId": "physical-product",
                        "name": "Blue shirt",
                        "url": "https://digitalriver.com/blue-shirt",
                        "countryOfOrigin": "US",
                        "image": "https://mdbootstrap.com/img/Photos/Horizontal/E-commerce/Vertical/12.jpg",
                        "weight": 20.5,
                        "weightUnit": "oz",
                        "partNumber": "Part123"
                    },
                    ...
                    "shipFrom": {
                        "address": {
                            "line1": "10380 Bren Rd W",
                            "city": "Minnetonka",
                            "postalCode": "55343",
                            "state": "MN",
                            "country": "US"
                        }
                    },
                    ...
                },
                {
                    "id": "185466050336",
                    "productDetails": {
                        "id": "physical-product-2",
                        "skuGroupId": "physical-product",
                        "name": "Red shirt",
                        "url": "https://digitalriver.com/red-shirt",
                        "countryOfOrigin": "US",
                        "image": "https://mdbootstrap.com/img/Photos/Horizontal/E-commerce/Vertical/12.jpg",
                        "weight": 20.5,
                        "weightUnit": "oz",
                        "partNumber": "Part123"
                    },
                    ...
                    "shipFrom": {
                        "address": {
                            "line1": "1234 5th Ave",
                            "city": "New York",
                            "postalCode": "10005",
                            "state": "NY",
                            "country": "US"
                        }
                    },
                    ...
                }
            ],
            "shippingChoice": {
                "amount": 10.98,
                "description": "Expedited Shipping",
                "serviceLevel": "Expedited",
                "taxAmount": 0.0
            },
            ...
        }
    },
    ...
}
```
{% endcode %}

## Displaying errors

The body of the [request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Shipping-Quotes/operation/listShippingMethodQuotes) Digital River sends to your server always has (1) `shipTo`, which contains the customer's designated `address` and, depending on their selected `country`, might also have `additionalAddressInfo` as well as (2) the details of each `items[]` the customer is purchasing.&#x20;

If your service checks this data and determines that it's invalid, perhaps because `line1` or `line2` indicate that the customer is trying to ship the goods to a P.O. Box and you don't support that or `additionalAddressInfo.neighborhood` isn't serviced by your carriers, then it can return an error.&#x20;

We'll then display that error's `message` in the checkout experience.&#x20;

What you need to do to get this message displayed depends on whether you're using [Prebuilt Checkout](using-a-shipping-endpoint.md#prebuilt-checkout) or [Components](using-a-shipping-endpoint.md#components).

### Prebuilt Checkout

When implementing this feature in [Prebuilt Checkout](drop-in-checkout.md), here are some things to keep in mind:

* Your server must return one of our [stock errors](using-a-shipping-endpoint.md#stock-errors).&#x20;
*   Don't modify the [stock error's](using-a-shipping-endpoint.md#stock-errors) `code`. If you do, then its `message` won't display in the checkout experience. Instead, users will be told that an unknown error occurred.\
    \


    <figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>
* Altering your error's `message` has no affect on what's shown to users. If its `code` matches one of our supported values, then that [stock error's](using-a-shipping-endpoint.md#stock-errors) `message` is displayed, unmodified, in the checkout experience.
* To get the `message` displayed, your server needs to respond with a status code of `400` or `409` and the error's `type` must be `bad_request` or `conflict`.
* Digital River blocks customers from advancing to the shipping choice selection stage until they correct the issue.
* The error's `message` isn't translated into the [checkout-session's](../../developer-resources/digital-river-api-reference/checkout-sessions.md) [`language`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#language). Rather, it's always rendered in English.&#x20;

#### Stock errors

The following lists the stock, preformatted errors that are available. For illustration purposes, we also show how each is rendered:

{% tabs %}
{% tab title="Invalid address" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "shipping_address_invalid",
            "parameter": "string",
            "message": "The shipping address provided is not valid."
        }
    ]
}
```

<figure><img src="../../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="P.O. boxes unsupported" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "shipping_address_POBox_invalid",
            "parameter": "string",
            "message": "Shipping to a PO Box is not allowed."
        }
    ]
}
```

<figure><img src="../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Invalid location" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "shipping_address_location_invalid",
            "parameter": "string",
            "message": "Shipping is not supported for the provided location."
        }
    ]
}
```

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Invalid subdivision" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "shipping_address_subdivision_invalid",
            "parameter": "string",
            "message": "Shipping is not supported for the provided subdivision."
        }
    ]
}
```

<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>


{% endtab %}
{% endtabs %}

### Components

If you're implementing this feature in [Components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/):

* The error returned by your service must have a `message`, but doesn't need a `code`.
* The value you assign to `message` is customizable.
* Any [valid HTTP status code](https://en.wikipedia.org/wiki/List\_of\_HTTP\_status\_codes) in the `4xx` or `5xx` range is accepted, but it's recommend that you send back a `400 Bad Request`.&#x20;

Digital River displays your error's `message` in the [address component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md). Before doing that, we don't translate it into the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) [`language`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#language) or perform any other operations on it.&#x20;

{% tabs %}
{% tab title="Error" %}
{% code title="400 Bad Request" %}
```json
{
    "errors": [
        {
            "message": "An error message that you define"
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="Address component" %}
<figure><img src="../../.gitbook/assets/Screenshot 2023-12-11 101101.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

In addition, if your response contains an error, that component's [`done()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md#submitting-the-address-component) function will return `false`, which, if your application is setup correctly, should block customers from proceeding to the [shipping choice selection stage](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/shipping-component.md).

For details, refer to [Controlling the checkout flow](implementing-a-components-checkout.md#controlling-the-checkout-flow).&#x20;
