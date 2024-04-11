---
description: Learn how to manage inventory items
---

# Managing inventory items

[Inventory items](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) are only used in [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/).

In the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model), you must [define an inventory item](managing-inventory.md#defining-an-inventory-item) and then [create the resource](managing-inventory.md#creating-and-updating-inventory-items). Once created, you can then [update](managing-inventory.md#creating-and-updating-inventory-items) or [delete](managing-inventory.md#deleting-inventory-items) the resource. In this model, you must also ensure that the [shared attributes](common-attributes.md#shared-attributes) of [SKU-inventory item pairs](common-attributes.md) remain synchronized.

In both the [distributed](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model) and the [orchestrated models](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), you use an inventory item's [unique identifier](managing-inventory.md#unique-identifier) to [check inventory levels](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/checking-inventory-levels.md), [request shipping quotes](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/using-shipping-quotes.md#requesting-shipping-quotes), and [reserve products](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/reserving-inventory-items.md) during checkout.

In the [distributed model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#distributed-model), you must use an inventory item's [unique identifier](managing-inventory.md#unique-identifier) when [creating a fulfillment order](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#creating-a-fulfillment-order).

## Defining an inventory item

The following are some of an inventory item's key definable attributes. For comprehensive specifications, refer to the [Inventory Items API reference documentation](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items).

### Unique identifier

An inventory item's unique identifier is represented by `id`.

When [creating inventory items](managing-inventory.md#creating-and-updating-inventory-items), if you don't specify `id`, Digital River generates a value for you.

However, the product identifier in your system should match the inventory item's `id` in our system. As a result, we recommend that you specify your own inventory `id` and that it matches your product's designated universally unique identifier.

### Country of origin

An inventory item's `countryOfOrigin` is a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard. Invalid country codes return a `400 Bad Request`:

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

### ECCN

An inventory item's `eccn` represents an [Export Control Classification Number](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn) (ECCN). This value determines whether:

* A product requires a US export/re-export license
* A product contains any other license requirements/restrictions
* A product has an end use which is prohibited by applicable export control laws

Digital River's [legal documentation](https://www.digitalriver.com/legal-information/) lists [ECCNs pre-approved](https://www.digitalriver.com/legal-other/approved-eccns/) for use in the Digital River APIs. In the table's description field, you may find additional requirements and restrictions that further limit the use of the ECCN.

{% hint style="danger" %}
Digital River can only resell products with these listed ECCNs. If you have a product with an ECCN that you'd like to be considered for addition to the list, please contact [Legal-compliance@digitalriver.com](mailto:Legal-compliance@digitalriver.com)
{% endhint %}

### Harmonized system code

An inventory item's `hsCode` represents a [Harmonized System code](https://www.trade.gov/harmonized-system-hs-codes).

The format of the code is `####.##.####`, where `#` represents a numeric digit between 0 and 9. The first six digits are mandatory. Any code longer than six digits but less than ten digits is optional and based on the country's preference. The period is not included in the character count.

Digital River only validates that the format of a Harmonized System code you provide is correct. We don't determine whether the code accurately classifies your product.

For example, the full ten-digit code for Jasmine rice in the United States is 1006.20.40.25. If that's the value you specify, we don't check to ensure your product fits into that category.

Incorrectly formatted `hsCode` values return a `400 Bad Request`:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "hsCode",
            "message": "'1234.56.YW' is not a valid HS code."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Manufacturer identifier and part number

An inventory item contains `manufacturerId` and `partNumber` fields.

The `manufacturerId` signifies the unique identifier of a part/product's manufacturer.

A manufacturer part number (MPN) is a unique code issued by manufacturers to identify a part/product. It is represented by `partNumber`.

MPNs are meant to be static identifiers of a part/product, universal to all distributors, wholesalers, and resellers. They allow customers to identify exact parts and protect themselves from counterfeits accurately.

If two parts/products originate from two manufacturers, each must have its own MPN. These identifiers are especially relevant for automotive and consumer electronics due to the numerous parts in these complex products.

### Allow oversell

You may decide to build your integration such that customers can reserve out-of-stock items or pre-order items not yet in stock. To do this, you can use an inventory item's `allowOversell` flag.

If you set the flag to `true`, customers can [reserve the item](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/reserving-inventory-items.md) even when inventory is not available. When set to `false`, customers won't be able to place a hold on an item when its inventory levels are insufficient.

{% hint style="info" %}
You can override `allowOversell` during the [product reservation process](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/reserving-inventory-items.md).
{% endhint %}

## Inventory Items API operations

You can use the [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) to [create and update](managing-inventory.md#creating-and-updating-inventory-items), [retrieve](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveInventoryItems), [search for](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listInventoryItems), and [delete inventory items](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteInventoryItems).

### Creating and updating inventory items

The [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) allows you to create and update inventory items.

{% hint style="warning" %}
In the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), do not directly create or update inventory items.

For more information, refer to [managed fulfillments](creating-and-updating-skus.md#managed-fulfillments) on the [Managing SKUs](creating-and-updating-skus.md) page.
{% endhint %}

The methods to create and update inventory items are similar, with one major difference. In [create requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createInventoryItems), you're allowed to specify a [unique identifier](common-attributes.md#unique-identifier). When [updating items](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateInventoryItems), you must send that identifier as a path parameter.

{% tabs %}
{% tab title="Create an inventory item" %}
```
curl --location --request POST 'http://api.digitalriver.com/inventory-items' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "id": "8d7b212f-2a19-4530-84b9-aa76e8dad4eb",
  "manufacturerId": "20013",
  "partNumber": "DEMOPARTNUMBER2",
  "eccn": "EAR99",
  "hsCode": "6404.20",
  "countryOfOrigin": "DK",
  "allowOversell": false
}'
```
{% endtab %}

{% tab title="Update an inventory item" %}
```
curl --location --request POST 'http://dispatch-test.digitalriver.com/inventory-items/8d7b212f-2a19-4530-84b9-aa76e8dad4eb' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "countryOfOrigin": "CA",
  "allowOversell": true
}'
```
{% endtab %}
{% endtabs %}

For both `POST/inventory-items` and `POST/inventory-items/{id}` requests, however, you can specify a [part number](managing-inventory.md#manufacturer-identifier-and-part-number), [Export Control Classification Number](managing-inventory.md#eccn), [Harmonized System code](managing-inventory.md#harmonized-system-code), and [country of origin](managing-inventory.md#country-of-origin). You can also tell us whether you want to [allow overselling](managing-inventory.md#allow-oversell) of that item.

### Retrieve inventory items

The [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) allows you to [retrieve a unique inventory item by its identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveInventoryItems)

### Searching inventory items

The [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) allows you to [search for inventory items using optional query parameters](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listInventoryItems).

### Deleting inventory items

The [Inventory Items API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Inventory-items) lets you permanently [delete an inventory item](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteInventoryItems) by supplying its unique identifier.

{% hint style="warning" %}
In [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/) that use the [orchestrated model](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/#orchestrated-model), you should not directly delete inventory items.

For more information, refer to [managed fulfillments](creating-and-updating-skus.md#managed-fulfillments) on the [Managing SKUs](creating-and-updating-skus.md) page.
{% endhint %}
