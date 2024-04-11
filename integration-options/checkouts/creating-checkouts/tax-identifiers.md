---
description: Learn how to manage and apply tax identifiers.
---

# Tax identifiers

{% hint style="warning" %}
In versions `2021-02-23` and later, use the features described on this page to manage tax identifiers. Once you upgrade to any of these versions, the tax identifiers you previously created through the [Customers API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) will no longer be available. Please contact us to have your data migrated.

For versions `2020-12-17` and earlier, refer to the [Tax identifiers (legacy)](../../../customer-management/setting-tax-related-attributes.md#tax-identifiers) section on the [Setting up tax exemptions page](../../../customer-management/setting-tax-related-attributes.md).
{% endhint %}

In the Digital River API, tax identifiers are used for [tax assessment and invoicing purposes](tax-identifiers.md#background).

When you [create a tax identifier](tax-identifiers.md#creating-tax-identifiers), we initiate a [validation process](tax-identifiers.md#how-we-validate-tax-identifiers). Once the [tax identifier object](tax-identifiers.md#the-tax-identifier-object) transitions to the appropriate [verification state](tax-identifiers.md#states-and-triggered-events), and assuming it's [applicable to the order](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders), it can be used to determine an order's taxability.

To [apply a tax identifier](tax-identifiers.md#applying-tax-identifiers), you can [attach it directly to a checkout or invoice](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices). Alternatively, you can [associate it with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers) and then [use it in registered checkouts](tax-identifiers.md#using-tax-identifiers-in-registered-checkouts).

Your checkout flow should also take into account that some [countries require tax identifiers](tax-identifiers.md#supported-tax-identifiers). When a customer in one of these countries doesn't supply a tax identifier, we block the order and [provide notification](tax-identifiers.md#missing-tax-identifier-notifications) of the problem.

When you're ready to evaluate your integration, you can use our [test tax identifiers](tax-identifiers.md#test-tax-identifiers).

## Background

In most value-added tax (VAT) schemes, _domestic sales_ to business customers are assessed tax and customers then take a credit for this tax paid when they complete their monthly or quarterly VAT return. In these cases, customers need the invoice to display their tax identifier so they can obtain this credit.

Alternatively, _cross-border sales_ to business customers are not assessed tax in most VAT schemes. Instead, in a practice called reverse charge, customers self-assess the tax while simultaneously taking a credit for the tax when they complete their monthly or quarterly VAT return. In these cases, the tax identifier is used to determine whether or not reverse charge applies to a specific order.

Additionally, in a limited number of cases, tax identifiers are collected because they are [required by a specific country’s tax authority](tax-identifiers.md#supported-tax-identifiers) for invoicing purposes.

## The tax identifier object

In the Digital River APIs, a tax identifier is always represented by a [unique identifier](tax-identifiers.md#unique-identifier). Additionally, the object will contain attributes that indicate its [type and value](tax-identifiers.md#type-and-value), its [state](tax-identifiers.md#states-and-triggered-events), and [created time](tax-identifiers.md#created-and-updated-time).

In some cases, a tax identifier may also include a [customer identifier](tax-identifiers.md#customer-identifier), a [verified name and address](tax-identifiers.md#verified-name-and-address), and an [updated time](tax-identifiers.md#created-and-updated-time).

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
    "createdTime": "2018-04-25T20:36:00Z",
    "updatedTime": "2018-04-28T22:16:00Z",
    "customerId": "5774321009",
    "type": "de",
    "value": "DE123456789",
    "state": "verified",
    "stateTransitions": {
        "verified": "2020-05-30T06:52:31.041Z",
        "pending": "2020-05-30T06:45:12.041Z"
    }
}
```
{% endtab %}
{% endtabs %}

### Unique identifier

A tax identifier is always returned with a unique `id`. Besides using this identifier to [retrieve](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveTaxIdentifiers) and [delete](tax-identifiers.md#deleting-tax-identifiers) a tax identifier, you can use it to [attach a tax identifier to a checkout](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices) or [associate it with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers).

### Customer identifier

The `customerId` is only returned when the tax identifier is [associated with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers).

### Type and value

The `type` attribute identifies the country that issued the tax identifier. The [available types](tax-identifiers.md#supported-tax-identifiers) typically consist of a lowercase, two-letter country code. However, there are some countries that have more than one `type` and these contain a suffix to the country code. For example, Brazil has tax identifiers with types of `br`, `br_ie`, and `br_natural`.

The `value` is assigned by the issuing country. Before [creating a tax identifier](tax-identifiers.md#creating-tax-identifiers), you can use the [tax identifier element](../../../developer-resources/reference/elements/tax-identifier-element.md) to help you validate its format. This element also lets you know whether a tax identifier is required in the country where the purchase is being made.

### States and triggered events

A tax identifier can be in a state of `pending`, `not_valid`, and `verified`. Its state is dependent on where it is in the [verification process](tax-identifiers.md#how-we-validate-tax-identifiers).

Each state transition causes a corresponding [event](../../../order-management/events-and-webhooks-1/events-1/) to be emitted whose `data.object` consists of the tax identifier.

| (1) When the tax identifier is...               | (2) its state transitions to... | (3) and a...event is emitted. |
| ----------------------------------------------- | ------------------------------- | ----------------------------- |
| under review by an external verification agency | `pending`                       | `tax_identifier.pending`      |
| determined to be valid                          | `verified`                      | `tax_identifier.verified`     |
| determined to be invalid                        | `not_valid`                     | `tax_identifier.not_valid`    |

A tax identifier in any state can be [attached directly to a checkout](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices) or [associated with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers). Before taking either action, your integration should ideally wait to receive the `tax_identifier.verified` event. However, a tax identifier in either a `pending` or `verified` state is used to determine an order's taxability.

Additionally, as it moves from one state to another, an [ISO8601](https://www.iso.org/iso-8601-date-and-time-format.html) formatted date and time is returned in the `stateTransitions` hash table.

### Verified name and address

During the tax identifier [verification process](tax-identifiers.md#how-we-validate-tax-identifiers), we sometimes are able to obtain the holder's `verifiedName` and `verifiedAddress`.

### Created and updated time

A tax identifier always contains a `createdTime`. When a tax identifier is [associated with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers), its [state changes](tax-identifiers.md#states-and-triggered-events), or the [holder's name and address](tax-identifiers.md#verified-name-and-address) is added, then the time these events occurred is reflected in the `updatedTime` field.

## How we validate tax identifiers

When a [`POST/ tax-identifiers`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers/operation/createTaxIdentifiers) request is submitted, Digital River initiates a validation process. As part of this process, we always validate the format of a tax identifier, whatever its country of origin. Incorrectly formatted tax identifiers return the following error:

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
 {
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "value",
            "message": "Tax identifier 'IT00121239990xxxx' invalid."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Prior to [creating a tax identifier](tax-identifiers.md#creating-tax-identifiers), you can [use the tax identifier element to perform validation](tax-identifiers.md#validating-tax-identifiers).
{% endhint %}

For European Union tax identifiers, commonly known as Value Added Tax (VAT) numbers, we use the [VAT Information Exchange System (VIES)](https://ec.europa.eu/taxation\_customs/vies/) to validate customer's data.

After a `POST /tax-identifiers` is submitted, Digital River provides VIES the data submitted in the request. VIES, in turn, transmits our validation query to the database of the relevant member state. The member state's reply to VIES indicates whether the number exists and, if so, whether it's valid. The reply may also include the [holder's name and address](tax-identifiers.md#verified-name-and-address). VIES then relays this information back to us.

{% hint style="warning" %}
VIES no longer verifies VAT numbers from Great Britain.
{% endhint %}

If VIES successfully responds before the [checkout is converted to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), then the [tax identifier's `state`](tax-identifiers.md#states-and-triggered-events) transitions to either `verified` or `not_valid` . This causes either a `tax_identifier.verified` or `tax_identifier.not_valid` [event](../../../order-management/events-and-webhooks-1/events-1/) to fire. If the number is verified, then the tax identifier is immediately applied to the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

In many situations, however, VIES responds slowly or is down for scheduled or unscheduled reasons. This means the tax identifier might not transition from `pending` to `verified` until after [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation. In these cases, we treat a `pending` tax identifier as being `verified` until we know otherwise. In other words, `pending` and `verified` tax identifiers are both used by Digital River to determine an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) taxability.

If VIES indicates a tax identifier is `not_valid`, then we don't use it to determine an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) taxability.&#x20;

A tax identifier's information is displayed on [invoices](../../../order-management/accessing-invoices-and-credit-memos.md#order-invoices), regardless of its `state`.&#x20;

For certain countries, we also apply validation algorithms defined by the local authority that issued the number.

## When tax identifiers can be applied to checkouts <a href="#when-tax-identifiers-can-be-applied-to-orders" id="when-tax-identifiers-can-be-applied-to-orders"></a>

Before a tax identifier can be successfully applied to a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), the [tax identifier type](tax-identifiers.md#type-and-value), the [customer type](../../../customer-management/setting-tax-related-attributes.md#customer-type), the [selling entity](selling-entities.md), and the country (a [ship to](providing-address-information.md#ship-to-address) country for [physical goods](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) or a [bill to](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/common-payment-objects.md#address-object) country for [digital goods](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital)) must [all be in agreement](tax-identifiers.md#supported-tax-identifiers).

{% hint style="warning" %}
With a few [notable exceptions](tax-identifiers.md#supported-tax-identifiers), most countries only allow `business` customers to apply tax identifiers.
{% endhint %}

For example, the following is a partial response to a `POST/orders` request. In this case, a tax identifier has been successfully applied. This is because the tax identifier's `type` is in agreement with the order's `shipTo.country` and the customer is a `business` entity.

{% tabs %}
{% tab title="201 Created" %}
```javascript
{
  "id": "9182309218",
  ...
  "customerId": "5774321009",
  ...
  "shipTo": {
       "address": {
            ...
            "country": "GB"
        },
        ...
  },
  "customerType": "business",
  ...
  "taxIdentifiers": [{
        "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
        "customerId": "5774321009",
        "type": "uk",
        "value": "GB123283536",
        "state": "verified",
        "stateTransitions": {
             "pending": "2020-05-13T11:00:00.000Z",
             "verified": "2020-05-15T16:00:00.000Z"
        },
        "verified_name": "A.C. Doyle Inc.",
        "verified_address": "Hudson House, 221B Baker Street, London",
        "createdTime": "2020-08-01T02:25:53Z",
        "updatedTime": "2020-08-01T05:47:21Z"
    }],
   ...
}
```
{% endtab %}
{% endtabs %}

If you were to submit another `POST/orders` request with the same settings—the only difference being that in the new request you specified a`shipTo.country` of `DK` (Denmark)—you'd receive a `409 Conflict` response. This is because customers holding tax identifiers issued by one country can't apply them to orders being shipped to a different country.

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "taxIdentifiers",
            "message": "Tax identifiers of type 'uk' are not applicable to this order."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## How we select tax identifiers

Digital River first searches for [applicable tax identifiers](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) that are directly [attached to a checkout or invoice](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices). This is true whether you're checking out a [guest customer](using-the-checkout-identifier.md#guest-checkouts-or-invoices) or a [registered customer](using-the-checkout-identifier.md#registered-checkouts-or-invoices).

However, when it's a registered checkout and that [customer has associated tax identifiers](tax-identifiers.md#attaching-tax-identifiers-to-customers) that are applicable, and those tax identifiers are not yet attached, we apply them as well.

If no tax identifiers are directly attached to a checkout or invoice, and it's a guest customer making the purchase, we don't use any tax identifiers when computing taxes.

## Managing tax identifiers

Before they are [applied to orders](tax-identifiers.md#applying-tax-identifiers), we provide you the ability to [validate the tax identifier](tax-identifiers.md#validating-tax-identifiers) information provided by customers. Once validated, you can use the [Tax Identifiers API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers) to [create](tax-identifiers.md#creating-tax-identifiers), [retrieve](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveTaxIdentifiers), [delete](tax-identifiers.md#deleting-tax-identifiers), and [search for](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listTaxIdentifiers) them.

You can also [attach tax identifiers to customers](tax-identifiers.md#attaching-tax-identifiers-to-customers) and then later, if necessary, [detach them](tax-identifiers.md#detaching-tax-identifiers-from-customers). To [reassign](tax-identifiers.md#reassigning-tax-identifiers) or [replace](tax-identifiers.md#replacing-a-customers-tax-identifier) tax identifiers, you must first delete the existing object before creating a new one.

### Validating tax identifiers

To validate the format entered by a customer and determine whether a tax identifier is both required and applicable to the transaction, you can use the [tax identifier element](../../../developer-resources/reference/elements/tax-identifier-element.md). To create the element, you must use some combination of the [selling entity](selling-entities.md) identifier, [payment session identifier](./#payment-session-identifier), and ship to/bill to [ISO 3166 country code](https://www.iso.org/iso-3166-country-codes.html) returned in a [Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [Invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices).

When you configure the element with a payment session identifier, we filter out tax identifiers that are not applicable to the transaction.

### Creating tax identifiers

You use the `POST/tax-identifiers` method to create a tax identifier. In the request, you must specify both a [type and value](tax-identifiers.md#type-and-value). Once the request is submitted, we initiate a [validation process](tax-identifiers.md#how-we-validate-tax-identifiers).

{% tabs %}
{% tab title="POST/tax-identifiers" %}
```
curl --location --request POST 'https://api.digitalriver.com/tax-identifiers' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "type": "de",
    "value": "DE123456789"
}'
```
{% endtab %}
{% endtabs %}

The following is an example `201 Created` response. It doesn't contain a `customerId` because the tax identifier hasn't been attached to a customer yet. The [pending state](tax-identifiers.md#states-and-triggered-events) of the tax identifier indicates it's still being [validated by an external agency](tax-identifiers.md#how-we-validate-tax-identifiers).

{% tabs %}
{% tab title="201 Created" %}
```javascript
{
    "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
    "createdTime": "2018-04-25T20:36:00Z",
    "updatedTime": "2018-04-28T22:16:00Z",
    "type": "de",
    "value": "DE123456789",
    "state": "pending",
    "stateTransitions": {
        "pending": "2020-05-30T06:45:12.041Z"
    }
}
```
{% endtab %}
{% endtabs %}

### Deleting tax identifiers

You can delete a tax identifier by submitting a `DELETE/tax-identifiers/{id}` request that sends its unique identifier as a path parameter. A successful request returns a `204 No Content` response. It also triggers a `tax_identifier.deleted` event and [detaches the tax identifier from any customer](tax-identifiers.md#detaching-tax-identifiers-from-customers) it may have been associated with.

Once a tax identifier is deleted, if you later attempt to [attach it to a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers), you'll get the following `404 Not Found` error.

{% tabs %}
{% tab title="404 Not Found" %}
```javascript
{
    "type": "not_found",
    "errors": [
        {
            "code": "not_found",
            "parameter": "id",
            "message": "Tax identifier '88b8fd94-14bd-4711-b381-9f73abef1546' not found."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Attaching tax identifiers to customers

Once you've [created a tax identifier](tax-identifiers.md#creating-tax-identifiers), you can use the `POST/customers/{id}/tax-identifiers/{taxId}` method to attach it to an existing customer. This request returns the [tax identifier](tax-identifiers.md#the-tax-identifier-object) and triggers a `customer.tax_identifier.created` event. The `data.object` of the event also represents the tax identifier.

Since it's now associated with a customer, the `customerId` attribute is populated in the response. The following example response shows a British (`uk`) issued tax identifier in a [verified state](tax-identifiers.md#states-and-triggered-events). When the customer next makes an [applicable purchase](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders), this tax identifier will be automatically applied to the order.

{% tabs %}
{% tab title="200 OK" %}
```javascript
{
    "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
    "customerId": "5774321009",
    "type": "uk",
    "value": "GB123283536",
    "state": "verified",
    "stateTransitions": {
         "pending": "2020-05-13T11:00:00.000Z",
         "verified": "2020-05-15T16:00:00.000Z"
    },
    "verified_name": "Royal Flushing Inc.",
    "verified_address": "Westminster, London SW1A 1AA, United Kingdom",
    "createdTime": "2020-08-01T02:25:53Z",
    "updatedTime": "2020-08-01T05:47:21Z"
}
```
{% endtab %}
{% endtabs %}

### Detaching tax identifiers from customers

To disassociate a tax identifier from a customer, send a [delete request](tax-identifiers.md#deleting-tax-identifiers) through the [Tax Identifiers API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers). A successful request means that when the customer creates [applicable](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) registered checkouts in the future, this tax identifier will no longer be applied.

### Reassigning tax identifiers

The same tax identifier object can't be attached to multiple customers. If you attempt to [associate a tax identifier with a customer](tax-identifiers.md#attaching-tax-identifiers-to-customers), but it's already attached to a different customer, you'll receive a `409 Conflict` response.

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "customer_not_updateable",
            "parameter": "customerId",
            "message": "You cannot replace a tax identifier's customer id."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

In these cases, you must first [delete the tax identifier](tax-identifiers.md#deleting-tax-identifiers), create a new object with an identical [type and value](tax-identifiers.md#type-and-value), and then assign it to the desired customer.

### Replacing a customer's tax identifier

Customers can have multiple tax identifiers, but they can't have more than one of the same [type](tax-identifiers.md#type-and-value). So if you'd like to attach a new tax identifier to a customer, but that customer already holds one with that `type`, you must first [delete the existing object](tax-identifiers.md#deleting-tax-identifiers). Once you've consumed either the `204 No Content` response or the `tax_identifier.deleted` event, your integration can then [create the new tax identifier](tax-identifiers.md#creating-tax-identifiers) and [attach it to the same customer](tax-identifiers.md#attaching-tax-identifiers-to-customers).

## Applying tax identifiers

Once they are created, there are two ways to apply tax identifiers to a purchase. You can either [attach the tax identifier directly to a checkout or invoice](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices). Or you can [use tax identifiers in registered checkouts](tax-identifiers.md#using-tax-identifiers-in-registered-checkouts).

In either case, during the checkout process, we determine whether the [tax identifier is applicable](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) and [notify you of missing tax identifiers](tax-identifiers.md#missing-tax-identifier-notifications).

You should also ensure you pass the necessary information to correctly [display the tax identifier on invoices](tax-identifiers.md#ensuring-tax-identifier-information-displays-on-invoices).

### Attaching tax identifiers to checkouts and invoices

When checking out both [registered and guest customers](using-the-checkout-identifier.md), you can attach tax identifiers directly to a checkout or invoice. You do this by using a `POST/checkouts`,`POST/checkouts/{id}`, or `POST/invoices` request and sending the object's identifier in the `taxIdentifiers` array.

{% tabs %}
{% tab title="POST/checkouts" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "customerId": 520984250336,
    ...
    "taxIdentifiers": [{
        "id": "2bba2529-97cb-4f0e-872f-5d97ac242cc0"
    }],
    ...
}'
```
{% endtab %}
{% endtabs %}

A successful response returns a checkout or invoice that contains an array of [tax identifier objects](tax-identifiers.md#the-tax-identifier-object). The [`state` of each tax identifier](tax-identifiers.md#states-and-triggered-events), which indicates whether it will be used to determine an order's taxability, depends on [how it is validated](tax-identifiers.md#how-we-validate-tax-identifiers).

{% tabs %}
{% tab title="201 Created" %}
```javascript
{
    "id": "1003189166920",
    ....
    "customerId": "520984250336",
    ...
    "shipTo": {
        "address": {
            "line1": "Neuschwansteinstraße 20",
            "city": "Schwangau",
            "postalCode": "87645",
            "country": "DE"
        },
        "organization": "Wagner,LLC",
        ...
    },
    ...
    "customerType": "business",
    ...
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "taxIdentifiers": [
        {
            "id": "2bba2529-97cb-4f0e-872f-5d97ac242cc0",
            "customerId": "520984250336",
            "type": "de",
            "value": "DE231287923",
            "state": "verified",
            "stateTransitions": {
                 "pending": "2020-12-23T16:00:00.000Z",
                 "verified": "2020-12-23T16:00:00.000Z"
            },
            "verifiedName": "Checkpoint Security Services Ltd.",
            "verifiedAddress": "Friedrichstraße 43-45, 10117 Berlin, Germany",
            "createdTime": "2020-12-23T15:21:26Z",
            "updatedTime": "2020-12-23T15:21:26Z"
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

For registered checkouts, any tax identifiers directly attached to the checkout must be associated with the customer placing the order. If any are held by a different customer, the following `409 Conflict` response is returned:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        { 
            "code": "tax_identifier_in_use", 
            "parameter": "taxIdentifiers", 
            "message": "Tax identifier 'a6809a63-e6a9-4016-abbc-f33d19fccb5b' is attached to a different customer." 
        }
    ]
}
```
{% endtab %}
{% endtabs %}

Before attaching a tax identifier, you should [determine whether it's applicable](tax-identifiers.md#filtering-applicable-tax-identifiers).

When using a customer's saved tax identifier, make sure you determine whether it exists. If you associate a tax identifier with a checkout, but the object has been deleted, we return the following error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "not_found",
            "parameter": "id",
            "message": "Tax identifier 'a6809a63-e6a9-5029-abbc-f66d19fccbcb' not found."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Using tax identifiers in registered checkouts

{% hint style="warning" %}
This information in this section is only applicable to [versions](../../../general-resources/versioning.md) `2021-03-23` and earlier of the Digital River APIs.

For more information, refer to [registered checkouts](using-the-checkout-identifier.md#registered-checkouts-or-invoices) on the [Checking out guest and registered](using-the-checkout-identifier.md) customers page.
{% endhint %}

When you create a [registered checkout](using-the-checkout-identifier.md#registered-checkouts-or-invoices), we search for [applicable](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) tax identifiers [attached to that customer](tax-identifiers.md#attaching-tax-identifiers-to-customers). If we locate any, they are automatically applied to the checkout or invoice and returned in its `taxIdentifiers` array.

{% hint style="info" %}
You can send an empty `taxIdentifiers` array to [instruct Digital River not to automatically apply tax identifiers](tax-identifiers.md#informing-digital-river-not-to-apply-tax-identifiers).
{% endhint %}

For example, let's say a [business](../../../customer-management/setting-tax-related-attributes.md#customer-type) customer holds a tax identifier of type `dk` (Denmark) and another of type `uk` (Great Britain). In a `POST/checkouts` request, you [associate this customer with the checkout](using-the-checkout-identifier.md#associating-a-checkout-or-invoice-with-an-existing-customer) and specify a [ship to country](providing-address-information.md#ship-to-address) of `GB`(Great Britain).

In this case, only the `uk` tax identifier is returned in the response. This is because tax identifiers are not applied to purchases when the [type and ship to country are not in agreement](tax-identifiers.md#supported-tax-identifiers).

{% tabs %}
{% tab title="201 Created" %}
```javascript
{
  "id": "9182309218",
  ...
  "customerId": "5774321009",
  ...
  "shipTo": {
       "address": {
            ...
            "country": "GB"
        },
        ...
  },
  "customerType": "business",
  ...
  "taxIdentifiers": [{
        "id": "a6809a63-e6a9-4016-abbc-f33d19fccb5b",
        "customerId": "5774321009",
        "type": "uk",
        "value": "GB000283536",
        "state": "verified",
        ...
    }],
   ...
}
```
{% endtab %}
{% endtabs %}

### Filtering applicable tax identifiers

If you attach a tax identifier to a checkout and the [necessary requirements](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) are not met, you receive an error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "taxIdentifiers",
            "message": "Tax identifier '0c38e49d-79d1-44a0-b484-472ca3f20cf3' is not applicable."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

To avoid this, you can apply a filter using the tax identifier's `applicability` block. This data structure contains the following attributes:

* `country`: The ship to country for [physical goods](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) or the bill to country for [digital goods](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital)
* `entity`: The [selling entity](selling-entities.md) of the transaction
* `customerType`: The [type of customer](setting-the-customer-type.md) making the purchase

Each attribute provides the required transaction values that must exist before a tax identifier can be successfully applied. In other words, the corresponding values in the checkout/invoice must be the same. If they're not, the tax identifier isn't applicable.

The `applicability` block is especially useful with [saved tax identifiers](tax-identifiers.md#saved-tax-identifiers). But, if for some reason you decide not to [use the tax identifier element as a filter](tax-identifiers.md#validating-tax-identifiers), you can also use `applicability` with [new tax identifiers](tax-identifiers.md#new-tax-identifiers).

#### Saved tax identifiers

During [registered checkouts](using-the-checkout-identifier.md#registered-checkouts-or-invoices), you can use `applicability` to filter customers' saved tax identifiers and display this filtered list to them on your site. Once the transaction's customer type is set and we've [assigned a selling entity](selling-entities.md#how-selling-entities-are-assigned), make a [`GET/customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCustomers) request to retrieve the customer's saved tax identifiers.

{% hint style="info" %}
In registered checkouts, you can send an empty `taxIdentifiers` array to [instruct Digital River not to automatically apply tax identifiers](tax-identifiers.md#informing-digital-river-not-to-apply-tax-identifiers).
{% endhint %}

In the following example, a customer has two saved tax identifiers. Both are applicable for `DR_IRELAND-ENTITY` facilitated transactions. The first tax identifier, however, is only appropriate for purchases made by individuals in Italy, while the other can be used for business transactions in the Netherlands.

Next, use the checkout's [`shipTo.country`](providing-address-information.md#ship-to-requirements) (or [`billTo.country`](providing-address-information.md#billing-address-requirements) for digital goods), `sellingEntity.id`, and `customerType`, along with the corresponding values in each of the customer's `applicability` blocks, to filter out the non-applicable tax identifiers.

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "541337030336",
    ...
    "taxIdentifiers": [
        {
            "id": "a19d26e7-8b7d-40e8-8358-b0a8b7203796",
            "state": "verified",
            "customerId": "541337030336",
            "type": "it_natural",
            "value": "IT5555555555",
            ...
            "applicability": [
                {
                    "country": "IT",
                    "entity": "DR_IRELAND-ENTITY",
                    "customerType": "individual"
                }
            ]
        },
        {
            "id": "6f5d4cb6-3c66-4a0b-a2aa-31cc25d3016d",
            "state": "verified",
            "customerId": "541337030336",
            "type": "nl",
            "value": "NL555555555555",
            ...
            "applicability": [
                {
                    "country": "NL",
                    "entity": "DR_IRELAND-ENTITY",
                    "customerType": "business"
                }
            ]
        }
    ],
    ...
    "type": "individual"
} 
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "5d0f0213-d8ab-4cc7-b721-1df1567df758",
    ...
    "customerId": "541337030336",
    ...
    "shipTo": {
        "address": {
            "line1": "Via del Governo Vecchio 87",
            "city": "Roma",
            "postalCode": "00186",
            "country": "IT"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "country": "GB"
        }
    },
    ...
    "customerType": "individual",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    ...
}
```
{% endtab %}
{% endtabs %}

After that, display this filtered list to the customer. Once the customer selects an option, [attach that tax identifier to the transaction](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices).

#### New tax identifiers

If a registered or [guest customer](using-the-checkout-identifier.md#guest-checkouts-or-invoices) supplies new tax identifier information during the checkout process, send the necessary data in a [`POST/tax-identifiers`](tax-identifiers.md#creating-tax-identifiers) request. You can then use `applicability` in the response to determine whether the checkout contains the matching country, selling entity, and customer type values.

{% hint style="success" %}
In this scenario, we suggest [using the tax identifier element to determine applicability](tax-identifiers.md#validating-tax-identifiers).
{% endhint %}

If it does, attach the tax identifier to the checkout. If not, inform the customer that they provided an ineligible tax identifier. In the following guest checkout, the customer supplied tax identifier is not applicable because the `customerType` values are not in agreement.

{% tabs %}
{% tab title="Tax Identifier" %}
```javascript
{
    "id": "a56be3b9-bdc1-4188-8ee9-b20b12264e48",
    "state": "verified",
    ...
    "type": "nl",
    "value": "NL555555555555",
    ...
    "applicability": [
        {
            "country": "NL",
            "entity": "DR_IRELAND-ENTITY",
            "customerType": "business"
        }
    ]
}
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "e4fca0fa-b303-4840-a912-e116abe746ca",
    ...
    "shipTo": {
        "address": {
            "line1": "Paulus Potterstraat 7",
            "city": "Amsterdam",
            "postalCode": "1071 DJ",
            "country": "NL"
        },
        ...
    },
    "shipFrom": {
        "address": {
            "country": "GB"
        }
    },
    ...
    "customerType": "individual",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    ...
}
```
{% endtab %}
{% endtabs %}

### Informing Digital River not to apply tax identifiers

When you want to inform us that no tax identifiers should be applied to a [registered checkout](using-the-checkout-identifier.md#registered-checkouts-or-invoices), submit a create or update request with an empty `taxIdentifiers` array. This indicates that none of the customer's [applicable tax identifiers](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders) should be used to determine the order's taxability.

For example, if a customer selects a saved tax identifier during the checkout process, but later deselects it, you can submit the following `POST/checkouts/{id}` request to ensure it's not applied.

{% tabs %}
{% tab title="POST/checkouts/{id}" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts/183731720336' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "customerId": 520984250336,
    ...
    "taxIdentifiers": [],
    ...
}'
```
{% endtab %}
{% endtabs %}

On the other hand, not including the`taxIdentifiers` array in a registered checkout has no affect. In this scenario, we [automatically apply](tax-identifiers.md#using-tax-identifiers-in-registered-checkouts) any applicable tax identifiers that are saved to the customer's account.

### Missing tax identifier notifications

For [some countries](tax-identifiers.md#supported-tax-identifiers), customers are required to provide a valid tax identifier when conducting online transactions. If customers in these countries don't provide this information, Digital River blocks their order from being placed.

{% hint style="info" %}
During the checkout process, you can use the [tax identifier element](../../../developer-resources/reference/elements/tax-identifier-element.md) to determine whether a tax identifier is required in the customer's country.
{% endhint %}

As an example, let's say a `POST/checkouts` request specifies a [customer type](../../../customer-management/setting-tax-related-attributes.md#customer-type) of `individual` and a [ship-to country](providing-address-information.md#ship-to-address) of `BR` (Brazil). In that same request, if no tax identifiers with a [`type`](tax-identifiers.md#type-and-value) of `br_natural` are either [attached directly to the checkout](tax-identifiers.md#attaching-tax-identifiers-to-checkouts-and-invoices) or [associated with the customer placing the order](tax-identifiers.md#using-tax-identifiers-in-registered-checkouts), you'll receive a `409 Conflict` response.

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "additional_information_required",
            "parameter": "taxIdentifiers",
            "message": "Tax identifiers of type 'br_natural' are required with this selling entity."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Ensuring tax identifier information displays on invoices

After an order is successfully fulfilled, and you've received the necessary events, you can [share the generated invoice with customers](../../../order-management/creating-and-updating-an-order.md#tax-invoices-and-credit-memos). When its a [business customer](../../../customer-management/setting-tax-related-attributes.md#customer-type) applying a tax identifier, the company name needs to be displayed on these invoices. To ensure this happens, you must set the `organization` parameter when [specifying a shipping address](providing-address-information.md#ship-to-address) for orders that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital).

## Supported tax identifiers

The following table lists the combination of [ship to](providing-address-information.md#ship-to-address) country, [tax id type](tax-identifiers.md#type-and-value), [customer type](../../../customer-management/setting-tax-related-attributes.md#customer-type), and [selling entity](selling-entities.md) that must be in alignment before a tax identifier can be applied to an order.

As the table indicates, most countries don't require a tax identifier when making an online purchase within their borders. For those that do, however, [customers can't conduct transactions](tax-identifiers.md#missing-tax-identifier-notifications) without first providing a valid tax identifier.

| Ship to country      | Tax id type   | Customer Type | Selling Entity      | Required? | Description                               |
| -------------------- | ------------- | ------------- | ------------------- | --------- | ----------------------------------------- |
| Australia            | `au`          | `business`    | `DR_IRELAND-ENTITY` | No        | ABN                                       |
| Austria              | `at`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Bahrain              | `bh`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Belarus              | `by`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Belgium              | `be`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Brazil               | `br`          | `business`    | `DR_BRAZIL-ENTITY`  | Yes       | Cadastro Nacional da Pessoa Jurídica      |
| Brazil               | `br_ie`       | `business`    | `DR_BRAZIL-ENTITY`  | Yes       | Inscrição Estadual                        |
| Brazil               | `br_natural`  | `individual`  | `DR_BRAZIL-ENTITY`  | Yes       | Cadastro de Pessoas Físicas (individuals) |
| Bulgaria             | `bg`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Canada               | `ca`          | `business`    | `DR_IRELAND-ENTITY` | No        | Canadian GST                              |
| Canada               | `ca`          | `business`    | `C5_INC-ENTITY`     | No        | GST Number                                |
| Chile                | `cl`          | `individual`  | `DR_IRELAND-ENTITY` | No        | RUT                                       |
| Chile                | `cl`          | `business`    | `DR_IRELAND-ENTITY` | No        | RUT                                       |
| Colombia             | `co`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Croatia              | `hr`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Cyprus               | `cy`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Czech Republic       | `cz`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Denmark              | `dk`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Estonia              | `ee`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Finland              | `fi`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| France               | `fr`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Germany              | `de`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Greece               | `gr`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Hungary              | `hu`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Iceland              | `is`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| India                | `in`          | `business`    | `DR_IRELAND-ENTITY` | No        | GSTIN                                     |
| Indonesia            | `id`          | `business`    | `DR_IRELAND-ENTITY` | No        | NPWP                                      |
| Ireland              | `ie`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Isle of Man          | `uk`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Isle of Man          | `uk`          | `business`    | `DR_UK-ENTITY`      | No        | VAT Number                                |
| Italy                | `it`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Italy                | `it_cf`       | `individual`  | `DR_IRELAND-ENTITY` | No        | Codice Fiscal (individuals)               |
| Italy                | `it_natural`  | `individual`  | `DR_IRELAND-ENTITY` | No        | VAT Number (individuals)                  |
| Japan                | `jp`          | `business`    | `DR_JAPAN-ENTITY`   | No        | TIN                                       |
| Japan                | `jp_offshore` | `business`    | `DR_IRELAND-ENTITY` | No        | Consumption Tax ID (offshore)             |
| Kenya                | `ke`          | `business`    | `DR_IRELAND-ENTITY` | Yes       | PIN                                       |
| Korea                | `kr_offshore` | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number (offshore)                     |
| Latvia               | `lv`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Lithuania            | `lt`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Luxembourg           | `lu`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Malaysia             | `my`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Malta                | `mt`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Mexico               | `mx_natural`  | `individual`  | `DR_IRELAND-ENTITY` | No        | RFC                                       |
| Mexico               | mx            | `business`    | `DR_IRELAND-ENTITY` | No        | RFC                                       |
| Monaco               | `fr`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Netherlands          | `nl`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| New Zealand          | `nz`          | `business`    | `DR_IRELAND-ENTITY` | No        | GST ID                                    |
| Norway               | `no`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Philippines          | `ph`          | `business`    | `DR_IRELAND-ENTITY` | No        | TIN                                       |
| Poland               | `pl`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Portugal             | `pt`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Portugal             | `pt_nif`      | `individual`  | `DR_IRELAND-ENTITY` | No        | NIF                                       |
| Romania              | `ro`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Russia               | `ru`          | `business`    | `DR_IRELAND-ENTITY` | No        | INN                                       |
| Russia               | `ru_natural`  | `business`    | `DR_IRELAND-ENTITY` | No        | INN                                       |
| Saudi Arabia         | `sa`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Singapore            | `sg`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Slovakia             | `sk`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Slovenia             | `si`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| South Africa         | `za`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Spain                | `es`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Sweden               | `se`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Switzerland          | `ch`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Taiwan               | `tw`          | `business`    | `DR_TAIWAN-ENTITY`  | Yes       | Unified Business Number                   |
| Taiwan               | `tw_offshore` | `business`    | `DR_IRELAND-ENTITY` | Yes       | Unified Business Number (offshore)        |
| Thailand             | `th`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Turkey               | `tr`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| Ukraine              | `ua`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| United Arab Emirates | `ae`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| United Kingdom       | `uk`          | `business`    | `DR_IRELAND-ENTITY` | No        | VAT Number                                |
| United Kingdom       | `uk`          | `business`    | `DR_UK-ENTITY`      | No        | VAT Number                                |

## Test tax identifiers

In the [test environment](../../../developer-resources/api-structure.md#test-and-production-environments), the following [`type` and `value`](tax-identifiers.md#type-and-value) pairs allow you to create [`verified`](tax-identifiers.md#states-and-triggered-events) tax identifiers:

| Country | `type`               | `value`                          |
| ------- | -------------------- | -------------------------------- |
| Belgium | `be`                 | `BE0000000000`, `BE1234567890`   |
| Germany | `de`                 | `DE000000000`, `DE123456789`     |
| Italy   | `it` or `it_natural` | `IT00000000000`, `IT12345678901` |

The Italian values can be paired with either `it` or `it_natural`. The `type` you specify depends on whether you're [applying the tax identifier](tax-identifiers.md#applying-tax-identifiers) to a test purchase made by an [`individual` or a `business`](setting-the-customer-type.md). Once you [create a test tax identifier](tax-identifiers.md#creating-tax-identifiers), you can always reference [`applicability`](tax-identifiers.md#filtering-applicable-tax-identifiers) to determine its [appropriate use](tax-identifiers.md#when-tax-identifiers-can-be-applied-to-orders).

{% tabs %}
{% tab title="Italy (individual)" %}
```javascript
{
    "id": "3234adc5-4857-4e48-8190-5a7d36843b89",
    "state": "verified",
    "liveMode": false,
    "type": "it_natural",
    "value": "IT12345678901",
    "stateTransitions": {
        "verified": "2021-09-02T18:44:55Z"
    },
    "createdTime": "2021-09-02T18:44:55Z",
    "updatedTime": "2021-09-02T18:44:55Z",
    "applicability": [
        {
            "country": "IT",
            "entity": "DR_IRELAND-ENTITY",
            "customerType": "individual"
        }
    ]
}
```
{% endtab %}

{% tab title="Italy (business)" %}
```javascript
{
    "id": "92d8984a-8c56-48a5-8cfd-c466ca8f3e62",
    "state": "verified",
    "verifiedName": "---",
    "verifiedAddress": "---",
    "liveMode": false,
    "type": "it",
    "value": "IT12345678901",
    "stateTransitions": {
        "verified": "2021-09-02T18:53:23Z"
    },
    "createdTime": "2021-09-02T18:53:23Z",
    "updatedTime": "2021-09-02T18:53:23Z",
    "applicability": [
        {
            "country": "IT",
            "entity": "DR_IRELAND-ENTITY",
            "customerType": "business"
        }
    ]
}
```
{% endtab %}
{% endtabs %}
