---
description: Understand how to describe a checkout's products or services
---

# Describing line items

You use a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `items[]` array to pass data on [products and/or services](../../../../product-management/skus.md) in a customer's cart. The elements of `items[]` allow you to:

* [Send product data](./#sending-product-data)
* [Set a product's price and quantity](./#setting-price-and-quantity)
* [Provide a product's subscription details](./#providing-subscription-information)
* [Discount a product](./#discounting-a-product)
* [Identify a product's ship from location](./#setting-a-ship-from-location)

After you [create a checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), we return an [`items[].id`](../#item-information) that uniquely identifies each of a checkout's line items. This identifier is needed to [modify the line item](./#updating-items) in a [update checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts).

Since update checkout requests only allow you to modify subscription, ship from and meta data, your create checkout request must include a line item's product data, price, and quantity.

For more information, refer to the [sending the create checkout request](../#sending-the-create-checkout-request) section on the [Building checkouts](../) page.

## Sending product data in checkouts <a href="#sending-product-data" id="sending-product-data"></a>

In [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), you must provide Digital River both [basic and compliance data](../../../../product-management/skus.md#basic-versus-compliance-product-data) on the products in a customer's cart. You have three options for passing this data. You can:

* [Send basic and compliance data in SKUs](./#send-basic-and-compliance-data-in-skus)
* [Send basic data in SKUs and compliance data in SKU groups](./#send-basic-data-in-skus-and-compliance-data-in-sku-groups)
* [Send basic data in `productDetails` and compliance data in SKU groups](./#send-basic-data-in-product-details-and-compliance-data-in-sku-groups)

Whichever option you select, [Digital River always returns `productDetails`](./#how-digital-river-returns-product-data).

{% hint style="info" %}
Digital River also assigns each of a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`items[]`](../#item-information) a unique `id`.&#x20;
{% endhint %}

### Send basic and compliance data in SKUs

In this option, prior to [checking out customers](../), you must define and create a [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) for each of the product's in your catalog. Each SKU needs to contain both [basic and compliance data](../../../../product-management/skus.md#basic-versus-compliance-product-data) on that product.

For more information, refer to the [Product basics](../../../../product-management/skus.md) and [Managing SKUs](../../../../product-management/creating-and-updating-skus.md) pages.

In this option, each `items[]` in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) must contain a `skuId`.

{% code title="POST/checkouts" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    ...
    "items": [
        {
            "skuId": "d0c6c536-1a5b-4c1d-be86-92e3363a1e1f",
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endcode %}

Once you submit this request, Digital River retrieves all the product data that we need from the referenced SKU.

This option requires you to keep the product catalog in your system synchronized with your SKUs in our system.

### Send basic data in SKUs and compliance data in SKU groups

In this option, prior to [checking out customers](../), you must define and create a [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) for each of the product's in your catalog. The SKUs only need to contain [basic product data](../../../../product-management/skus.md#basic-versus-compliance-product-data).

Before [creating checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), you must also [associate a SKU group with each of your SKUs](../../../../product-management/setting-up-sku-groups.md#using-sku-groups-in-transactions) by setting the [SKU's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) `skuGroupId`. The [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) holds the [product's compliance data](../../../../product-management/skus.md#basic-versus-compliance-product-data).

For more information, refer to:

* [Product basics](../../../../product-management/skus.md)
* [Managing SKUs](../../../../product-management/creating-and-updating-skus.md)
* [Grouping SKUs](../../../../product-management/setting-up-sku-groups.md)

In this option, each `items[]` in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) must contain a `skuId`.

{% code title="POST/checkouts" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    ...
    "items": [
        {
            "skuId": "d0c6c536-1a5b-4c1d-be86-92e3363a1e1f",
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endcode %}

Once you submit this request, Digital River retrieves basic product data from the referenced SKU and compliance product data from the SKU's SKU group.

This option requires that you keep the product catalog in your system synchronized with your SKUs in our system.

#### Common attributes and data priority in SKUs and SKU groups

If you decide to use this option, you should be aware that the following attributes are common to both [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) and [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups):

* Harmonized system code
* Export control classification number
* Tax code

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), a SKU group's data takes precedence over a SKU's data. If a common attribute is defined in a SKU, but not the SKU group it belongs to, then we use the SKU's data in the checkout.

For more details, refer to [Migrating to SKU groups](../../../../product-management/setting-up-sku-groups.md#migrating-to-sku-groups) on the [Grouping SKUs](../../../../product-management/setting-up-sku-groups.md) page.

### Send basic data in product details and compliance data in SKU groups

In this option, you don't store [basic product data](../../../../product-management/skus.md#basic-versus-compliance-product-data) in Digital River's system.

Instead, you retrieve this data from your system and, for each `items[]` in a [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), use it to define [`productDetails`](../../../../product-management/using-product-details.md) .&#x20;

{% hint style="success" %}
The [`id`](../../../../product-management/using-product-details.md#unique-identifier) in `productDetails` should be the same as the identifier of the product in your system.
{% endhint %}

The [`productDetails`](../../../../product-management/using-product-details.md) object must also contain a `skuGroupId` that references the [SKU group](../../../../product-management/setting-up-sku-groups.md) that holds the [product's compliance data](../../../../product-management/skus.md#basic-versus-compliance-product-data).

Digital River then accesses basic product data from `productDetails` and compliance data from the referenced SKU group.

{% code title="POST/checkouts" %}
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
            }
            "quantity": 2,
            "price": 10
        }
    ]
}'
```
{% endcode %}

Since you're not persisting any basic product data in Digital River's system, you're not required to keep the product catalog in your system synchronized with [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) in our system.

Prior to deployment however you do need to work with Digital River to [define your SKU groups](../../../../product-management/setting-up-sku-groups.md#defining-and-managing-sku-groups). Once defined, Digital River is responsible for managing the data in this resource.

For more information, refer to the [Grouping SKUs](../../../../product-management/setting-up-sku-groups.md) page.

#### Common attributes in `productDetails` and SKUs

If your integration currently uses [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs), and you're considering a migration to this option, you should be aware that the attributes in SKUs and [`productDetails`](../../../../product-management/using-product-details.md) are nearly identical.

The key exceptions are `taxCode`, `eccn`, and `hsCode`. These attributes exist in SKUs but not in `productDetails`. This is because all of these attributes contain [compliance data](../../../../product-management/skus.md#basic-versus-compliance-product-data) which is saved in the associated [SKU group](../../../../product-management/setting-up-sku-groups.md).

{% hint style="info" %}
SKUs also have a [`manufacturerId`](../../../../product-management/creating-and-updating-skus.md#manufacturer-id-and-part-number) and this attribute is not in `productDetails`.

In [Digital River coordinated fulfillments](../../../../order-management/fulfillments.md#digital-river-coordinated-fulfillments), `manufacturerId` is used to set up products in warehouses. That process however is handled prior to deployment. So there's no need to set `manufacturerId` in checkouts.
{% endhint %}

### How Digital River returns product data

Whether you send `productDetails` or `skuId` in [`POST/ checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), the `201 Created` response always contains `productDetails`.&#x20;

If you pass `productDetails`, we give you back that same data.&#x20;

But if your integration sends `skuId`, Digital River retrieves [basic product data](../../../../product-management/skus.md#basic-versus-compliance-product-data) from the referenced [SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) (along with that object's identifier), and uses it to populate the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `productDetails`. If you [convert the checkout to an order](../../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), `productDetails` is also passed through to that object.

{% tabs %}
{% tab title="POST/checkouts" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
...
--data-raw '{
    ...
    "items": [
        {
            "skuId": "b0fd7334-8f7d-424e-b535-308fae972461",
            "quantity": 2,
            "price": 10
        }
    ],
    ...
}'
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "08720898-5998-4501-aee6-f35d58de5e0a",
    ...
    "items": [
        {
            "id": "9f8bf171-8612-46c3-8d26-c37a4c710beb",
            "skuId": "b0fd7334-8f7d-424e-b535-308fae972461",
            "productDetails": {
                "id": "b0fd7334-8f7d-424e-b535-308fae972461",
                "name": "Widget",
                "description": "A small gadget or mechanical device",
                "countryOfOrigin": "US",
                "weight": 10,
                "weightUnit": "g",
                "partNumber": "b0fd7334-8f7d-424e-b535-308fae972461"
            },
            ...
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "231388420336",
    ...
    "items": [
        {
            "id": "158140150336",
            "skuId": "b0fd7334-8f7d-424e-b535-308fae972461",
            "productDetails": {
                "id": "b0fd7334-8f7d-424e-b535-308fae972461",
                "name": "Widget",
                "description": "A small gadget or mechanical device",
                "countryOfOrigin": "US",
                "weight": 10,
                "weightUnit": "g",
                "partNumber": "b0fd7334-8f7d-424e-b535-308fae972461"
            },
            ...
        }
    ],
    ...
    "checkoutId": "08720898-5998-4501-aee6-f35d58de5e0a"
}
```
{% endtab %}
{% endtabs %}

As a result, in both [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), as well as their associated [events](../../../../order-management/events-and-webhooks-1/events-1/), such as `checkout.updated`, [`order.complete`](../../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event), and [`subscription.reminder`](../../subscriptions/digital-river-coordinated-subscriptions.md#sending-a-reminder), you can easily access product data without having to make another [call to retrieve the SKU](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSkus).&#x20;

This feature is especially useful if you employ a third-party service that sends emails and other notifications to customers. These services can [configure a webhook](../../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#step-3.-create-webhooks) to listen for [events](../../../../order-management/events-and-webhooks-1/events-1/) such as [`order.fulfilled`](../../../../order-management/informing-digital-river-of-a-fulfillment.md#the-order-fulfilled-event) , [`order.cancelled`](../../../../order-management/creating-and-updating-an-order.md#the-order-cancelled-event), and [`order.complete`](../../../../order-management/informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event), and then handle these events by retrieving data from `productDetails` and passing it in the notification.&#x20;

## Setting price and quantity

For each element in a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `items[]` array, you must specify `quantity`. This represents the number of items selected by the customer. If you don't specify `quantity`, then its value defaults to `1`.

You must also set the line item's `price` or `aggregatePrice`.

For more information on how to do this, refer to the [Setting the price of an item](price-of-an-item.md) page.

## Providing subscription information

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you set `subscriptionInfo` at the line-item level. For more information, refer to:

* [Subscription information](../../subscriptions/subscription-information-1.md)
* [Digital River's subscription service](../../subscriptions/digital-river-coordinated-subscriptions.md)
* [Third party subscription services](../../subscriptions/third-party-coordinated-subscriptions.md)

## Discounting a product

For each element in a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `items[]` array, you can set a product-level `discount`.

For more information, refer to the [product discounts](../applying-a-discount.md#product-discounts) section on the [Applying a discount](../applying-a-discount.md) page.

## Setting a ship from location

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) products are shipping from multiple locations, you can specify each location using `items[].shipFrom`.

For more information, refer to the [ship from address](../providing-address-information.md#ship-from-address) section on the [Providing address information](../providing-address-information.md) page.

## Updating items

When updating products or services in a `POST/checkouts/{id}` request, you need to provide the [line item identifier](../#item-information) returned in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

For each line item in the update checkout request, you're restricted to updating [subscription information](../../subscriptions/subscription-information-1.md#setting-subscription-information), a product's [ship from address](../providing-address-information.md#ship-from-address), and `metadata`.

If you attempt to update any other line item data, you receive a `400 Bad Request`:

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "unknown_parameter",
            "parameter": "price",
            "message": "'price' is an unknown parameter."
        }
    ]
}
```
{% endtab %}
{% endtabs %}
