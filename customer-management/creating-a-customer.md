---
description: Learn how to create and update a customer.
---

# Creating and updating customers

Once you [define a customer](creating-a-customer.md#defining-a-customer), you can [create a customer object](creating-a-customer.md#creating-a-customer) and then [associate the object with checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices). Once the object is created, you can [save one or more payment sources](../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers) to a customer as well as [set a customer's default payment source](creating-a-customer.md#default-payment-source).

![](<../.gitbook/assets/Customer-object (1).png>)

## Defining a customer

The following provides guidance on how to define a customer. For complete specifications, refer to the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) reference documentation.

### Unique identifier

A customers  `id` must be forty characters or less in length. Anything longer, and a `400 Bad Request` with a `code` of `invalid_parameter` is returned.&#x20;

We recommend that a customer's identifier be identical in both your system and our system.

If you don't provide us an `id` value in the create customer request, we generate one for you and return it in the response.

### Email

The `email` parameter represents a customer's email address. You can create multiple customers in your account that contain identical `email` values.

### Shipping address

You can use `shipping` to store a customer's `name`, `phone`, `email`, `organization`, basic ship to `address`, and detailed ship to `additionalAddressInfo`.

### Tax identifiers and certificates

Every customer can store one or more [tax identifiers](setting-tax-related-attributes.md#tax-identifiers) and [tax certificates](setting-tax-related-attributes.md#tax-certificates).

### Locale

A customer's `locale` is used to [localize invoices and credit memos](../integration-options/checkouts/creating-checkouts/designating-a-locale.md).

### Customer type

A customer's `type` allows you to [differentiate between business and individual customers](setting-tax-related-attributes.md#setting-the-customer-type).

### Enabling a customer

If you set a customer's `enabled` flag to `false`, then any attempts to create orders that reference this customer will fail. You should only set `enabled` to `false` when you want to block a customer from placing orders. For example, you may decide this is necessary when a customer has a history of fraudulent behavior.

### Default payment source

The `defaultSourceId` should reference a [source](../payments/payment-sources/) that customers have indicated is their default payment instrument.

For more information, refer to [setting the default payment source](../payments/payment-sources/using-the-source-identifier.md#setting-the-default-payment-source) on the [Managing sources](../payments/payment-sources/using-the-source-identifier.md) page.

### Request to be forgotten

In [update customer requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCustomers), you can use `requestToBeForgotten` to instruct Digital River to delete a customer's data from our system.

For more information, refer to the [Recording a customer's request to be forgotten](../administration/dashboard/customers/removing-a-customers-personal-information.md) page.

## Creating a customer

The process of creating and updating a customer is similar. In a [create customer request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCustomers), you're allowed to specify the object's unique identifier. However, when [updating a customer](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCustomers) you must pass in this unique identifier as a path parameter.

An update customer request also allows you to [record a customer's right to be forgotten](creating-a-customer.md#request-to-be-forgotten).

The following `POST/customers` request specifies a unique `id`:

{% tabs %}
{% tab title="POST/customers" %}
```
curl --location --request POST 'https://api.digitalriver.com/customers' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
  "id": "5823594806",
  "email": "jsmith@digitalriver.com",
  "shipping": {
    "address": {
      "line1": "10380 Bren Rd W",
      "line2": "string",
      "city": "Minnetonka",
      "postalCode": "55129",
      "state": "MN",
      "country": "US"
    },
    "name": "John Smith",
    "phone": "952-111-1111",
    "email": "jsmith@digitalriver.com",
    "organization": "Digital River"
  },
  "type": "individual",
  "metadata": {
    "coupon": "iOS"
  },
  "locale": "en_US",
  "enabled": true
}'
```
{% endtab %}
{% endtabs %}

A successful request returns a `201 Created` whose payload contains a customer object:

{% tabs %}
{% tab title="201 Created" %}
```javascript
{
    "id": "5823594809",
    "createdTime": "2020-05-06T22:28:01Z",
    "email": "jsmith@digitalriver.com",
    "shipping": {
        "address": {
            "line1": "10380 Bren Rd W",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        },
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com"
    },
    "enabled": true,
    "requestToBeForgotten": false,
    "locale": "en_US",
    "type": "individual",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

Once you create a customer, you can the reference this object in [registered checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices).
