---
description: Learn how to retrieve the available quantity and time of inventory items.
---

# Checking inventory levels

In [Digital River coordinated fulfillments](./), you can call the [Inventory Levels API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels) to access product availability information at individual warehouses. After you [submit an inventory level request](checking-inventory-levels.md#submitting-an-inventory-level-request), each [inventory level object](checking-inventory-levels.md#an-inventory-level) contained in the response is associated with one [inventory item](../../../product-management/skus.md#inventory-items) and one location.

You can [use an inventory level](checking-inventory-levels.md#using-an-inventory-level) to [sequence your checkout](../creating-checkouts/) and provide product availability information to customers.

## Submitting an inventory level request

When you submit a [`GET/inventory-levels`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listInventoryLevels) request, you're required to provide an array of [inventory item identifiers](../../../product-management/common-attributes.md#unique-identifier) as a query parameter.

You can also filter the results by when inventory levels were last updated, whether the product is available, and which warehouse locations can ship the product to a specific country.

If you don't apply any filters, each inventory item identifier you specify in the request returns one or more [inventory level objects](checking-inventory-levels.md#an-inventory-level). However, the application of search filters, such as `available` or `shipToCountry`, may result in your query returning no results. For example, when you use the `shipToCountry` filter (which must be formatted as an [ISO 3166 country code](https://www.iso.org/iso-3166-country-codes.html)), you'll only get inventory level information if the product can be shipped to that country.

## **An inventory level**

After you successfully submit a [`GET/inventory-levels`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listInventoryLevels) request, a `200 OK` response contains a `data` array. Each element of this array represents an [inventory level](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels).

When a product is located at a single warehouse, you get back one [inventory level](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels). However, when an product is warehoused at multiple locations, we provide the [inventory level](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels) at each location.

An [inventory level](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-levels) provides the [unique identifier](../../../product-management/managing-inventory.md#unique-identifier), [warehouse location](checking-inventory-levels.md#product-location) and [availability](checking-inventory-levels.md#product-availability) of an [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items). The object also indicates when the inventory level was last updated.

{% tabs %}
{% tab title="Inventory level" %}
```javascript
{
  "data": [
    {
      "locationId": "afe95639-8181-4b66-86a6-1a9493d5419d",
      "inventoryItemId": "ce4ce2de-530c-4da2-bf8a-f0f8cf059095",
      "available": true,
      "availableQuantity": 6,
      "liveMode": false,
      "updatedTime": "2018-04-25T20:36:00Z"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

### Product location

The `locationId` represents the identifier of the fulfiller's warehouse that contains the [inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items).

### Product availability

If the product is `available`, then the `availableQuantity` of the inventory level is greater than zero. In these cases, `availableTime` is null and not returned.

If `available` is `false`, then `availableTime` provides an estimated time when the product is scheduled for restocking (assuming the fulfiller has provided this information). When the fulfiller doesn’t provide an estimated restocking time, then `availableTime` is null and not returned.

## Using an inventory level

You can use an [inventory level](checking-inventory-levels.md#an-inventory-level) to provide product availability information to customers. During the [checkout process](../creating-checkouts/), it can help you determine when to display or conceal a product on your storefront, notify customers when an item is almost out of stock or when it will be available again, display the remaining number of products in stock, and determine if an item is available for shipping to a specific country.

As an example, let's say you want to determine the availability of a coffee maker and whether it can be shipped to Sweden. To do this, submit a `GET/inventory-levels` that specifies the [inventory item identifier](../../../product-management/managing-inventory.md#unique-identifier), the `shipToCountry` as `SE`, and sets `available` to `true`.

{% tabs %}
{% tab title="GET/inventory-levels" %}
```
curl --location --request GET 'https://api.digitalriver.com/inventory-levels?inventoryItemIds=310abe81-69f6-44e5-85df-2674045e5460&shipToCountry=SE&available=true' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endtab %}
{% endtabs %}

In this case, Digital River determines a machine that can be shipped to Sweden is only available at one location, so the response returns just a single inventory level object.

{% tabs %}
{% tab title="Inventory level" %}
```javascript
{
    "data": [
        {
            "locationId": "20045",
            "inventoryItemId": "310abe81-69f6-44e5-85df-2674045e5460",
            "available": true,
            "availableQuantity": 995,
            "updatedTime": "2021-01-12T06:55:14Z",
            "liveMode": false
        }
    ]
}
```
{% endtab %}
{% endtabs %}

Your integration can also use an inventory level to determine whether to [reserve an inventory item](reserving-inventory-items.md) or [create a fulfillment order](global-fulfillments.md#creating-a-fulfillment-order).
