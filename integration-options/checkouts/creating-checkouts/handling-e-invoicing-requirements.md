---
description: >-
  Gain a better understanding of how to comply with e-invoicing requirements in
  Taiwan
---

# Handling e-invoicing requirements

If you select the [Direct integrations](../) option and you'd like to use the [e-invoicing service](../../../using-our-services/e-invoicing.md), this article outlines one possible approach you might use to handle a [guest checkout](using-the-checkout-identifier.md#guest-checkouts-or-invoices) that is assigned a [`sellingEntity.id`](selling-entities.md) of `DR_TAIWAN-ENTITY`.

{% hint style="info" %}
In [registered checkouts](using-the-checkout-identifier.md#registered-checkouts-or-invoices), your application can implement additional operations that save and/or retrieve a customer's [tax identifier](tax-identifiers.md).&#x20;
{% endhint %}

Before or after customers initiate checkout, use a control (such as a radio button or checkbox) to determine whether they're making the purchase as an individual or on behalf of a business. Depending on the customer's selection, display the appropriate fields in your shipping and/or billing information collection form.&#x20;

![](<../../../.gitbook/assets/e-Invoicing (Taiwan only).jpeg>)

If customers are making the purchase as a business entity, then your form needs to collect their organization/company name. Otherwise, that field isn't needed.&#x20;

![](<../../../.gitbook/assets/image (15).png>)

Add a click event handler to the form's submit button that uses the data it collects to set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`customerType`](setting-the-customer-type.md), [`shipTo`](providing-address-information.md#ship-to-address) and/or [`billTo`](providing-address-information.md#bill-to-address).

{% hint style="warning" %}
If `customerType` is `business`, then make sure you define `shipTo.organization` and/or `billTo.organization`.&#x20;
{% endhint %}

{% code title="POST /checkouts/{id}" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts/7890d7c5-e15a-4827-80b0-8652de82ad04' \
...
--header 'Authorization: Bearer <Secret API Key>' \
...
--data-raw '{
    "customerType": "business",
    "shipTo": {
        "address": {
            "line1": "台南市安平區光州路3號",
            "city": "Tainan",
            "postalCode": "708",
            "state": "Taiwan",
            "country": "TW"
        },
        "name": "John Doe",
        "organization": "Acme, Inc."
    },
    "billTo": {
        "address": {
            "line1": "台南市安平區光州路3號",
            "city": "Tainan",
            "postalCode": "708",
            "state": "Taiwan",
            "country": "TW"
        },
        "name": "John Doe",
        "organization": "Acme, Inc."
    }
}'
```
{% endcode %}

In the response, determine whether [`sellingEntity.id`](selling-entities.md) is `DR_TAIWAN-ENTITY`.&#x20;

{% code title="Checkout" %}
```javascript
{
    "id": "7890d7c5-e15a-4827-80b0-8652de82ad04",
    ...
    "customerType": "individual",
    ...
    "sellingEntity": {
        "id": "DR_TAIWAN-ENTITY",
        "name": "Digital River Taiwan"
    },
    ...
}
```
{% endcode %}

If it is, determine the value of `customerType`.

If `customerType` is `individual`, retrieve [`payment.session.id`](payment-sessions.md), use it to set `sessionId` in the [invoice attribute element's](../../../developer-resources/reference/elements/invoice-attribute-element.md) configuration object, and then [create](../../../developer-resources/reference/elements/invoice-attribute-element.md#createelement-invoiceattribute-options) and [mount](../../../developer-resources/reference/elements/invoice-attribute-element.md#mount) that element. When [on complete](../../../developer-resources/reference/elements/invoice-attribute-element.md#on-complete-handler) executes, retrieve `id` from the event's payload and pass it as `invoiceAttributeId` in the body of an [update checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts).&#x20;

In B2C transactions, if your [create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) contains no `invoiceAttributeId`, then Digital River returns a `409 Conflict`.&#x20;

```json
{
    "type": "conflict",
    "errors": [
        {
            "code": "additional_information_required",
            "parameter": "invoiceAttributeId",
            "message": "Invoice attribute is required."
        }
    ]
}
```

If `customerType` is `business`, retrieve `payment.session.id`, use it to set `sessionId` in the [tax identifier element's](../../../developer-resources/reference/elements/tax-identifier-element.md) configuration object and then [create](../../../developer-resources/reference/elements/tax-identifier-element.md#creating-a-tax-identifier-element) and mount the element. Handle [on change](../../../developer-resources/reference/elements/tax-identifier-element.md#change) by checking the event's payload to determine whether `elementType` is `taxidentifier` and `complete` is `true`. If that's the case, retrieve `identifier.type` and `identifier.value` and pass them as `type` and `value` in the body of a [create tax identifier request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Tax-identifiers/operation/createTaxIdentifiers). From the response, retrieve `id` and pass it as `taxIdentifiers[].id` in the body of an [update checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts).&#x20;

In B2B transactions, if your [create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) contains no `taxIdentifiers[].id`, then Digital River returns a `409 Conflict`.&#x20;

```json
{
    "type": "conflict",
    "errors": [
        {
            "code": "additional_information_required",
            "parameter": "taxIdentifiers",
            "message": "Tax identifiers with types of 'tw' are required."
        }
    ]
}
```

Once you've completed either of these operations, you can collect the customer's shipping choice (when required) and payment. For details refer to:

* [Handling shipping quotes](./#handling-shipping-quotes)
* [Drop-in payments integration guide](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md)
* [DigitalRiver.js with Elements integration guide](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md)
* The **Payment methods for Taiwan** section in the [Taiwan country guide](https://www.digitalriver.com/global-availability/taiwan/)

After you create the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), initiate [fulfillment operations](../../../order-management/fulfillments.md), and then receive the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../../order-management/events-and-webhooks-1/events-1/#event-types) of [`order.complete`](../../../order-management/events-and-webhooks-1/events-1/event-types.md#order.complete), you could use its [`data.object`](../../../order-management/events-and-webhooks-1/events-1/#event-data) to build an order summary page on your site.&#x20;

As part of that operation, you can determine whether the event's [`data.object`](../../../order-management/events-and-webhooks-1/events-1/#event-data) contains `invoiceAttribute` or `taxIdentifiers[]`.

If `invoiceAttribute` is populated, then you can display each of its `attributes` on the summary page.  Similarly, if a `taxIdentifiers[]` exists, you can display its `value` on that same page. &#x20;

{% hint style="success" %}
Digital River has integrated with a third-party service that gives customers access to all of their eGUIs. As a result, you're not required to provide this information on your site.  \
\
In B2C transactions, the service adds the eGUIs to a customer-accessible website managed by the government. In B2B transactions, customers are sent an email that contains the eGUI number, a link to the national lottery site, and a PDF attachment of the invoice.
{% endhint %}

For each `invoiceAttribute.type`, the following provides an example of the data contained in `order.complete`.

{% tabs %}
{% tab title="tw_individual_mobile_barcode" %}
{% code title="order.complete" %}
```javascript
{
    "id": "32d36468-9c01-49a2-a4d1-31f5abf01308",
    "type": "order.complete",
    "data": {
        "object": {
            "id": "231067550336",
            ...
            "invoiceAttribute": {
                "id": "d9c6e7b2-3646-418b-8afa-a8cc9e86feda",
                "type": "tw_individual_mobile_barcode",
                "attributes": {
                    "MOBILE_BARCODE": "/ABC+123"
                },
                ...
            },
            ...
        }
    },
    ...
```
{% endcode %}
{% endtab %}

{% tab title="tw_individual_member_carrier" %}
{% code title="order.complete" %}
```javascript
{
    "id": "b8da3ffc-6d40-4e7b-9677-eb0ab28525c4",
    "type": "order.complete",
    "data": {
        "object": {
            "id": "230957950336",
            ...
            "invoiceAttribute": {
                "id": "9557110c-b0ff-4ca3-bb3a-7f0711c31a86",
                "type": "tw_individual_member_carrier",
                "attributes": {
                    "MEMBER_CARRIER": "test@mail.com"
                },
                ...
            },
            ...
        }
    },
    ...
}
```
{% endcode %}
{% endtab %}

{% tab title="tw_individual_citizen_cert" %}
{% code title="order.complete" %}
```javascript
{
    "id": "3e18abe0-8b84-4cd8-ab61-154f109319a8",
    "type": "order.complete",
    "data": {
        "object": {
            "id": "230957170336",
            ...
            "invoiceAttribute": {
                "id": "6817148d-09eb-451e-b17e-3c47d7e7ff36",
                "type": "tw_individual_citizen_cert",
                "attributes": {
                    "CITIZEN_DIGITAL_CERT": "AB12345678901234"
                },
                ...
            },
            ...
        }
    },
    ..."
}
```
{% endcode %}
{% endtab %}

{% tab title="tw_individual_donate" %}
{% code title="order.complete" %}
```javascript
{
    "id": "4276f7cf-a298-4c1c-b13c-c8cfe4be1077",
    "type": "order.complete",
    "data": {
        "object": {
            "id": "230958000336",
            ...
            "invoiceAttribute": {
                "id": "97144bc7-babb-435d-a4ff-eebac26196df",
                "type": "tw_individual_donate",
                "attributes": {
                    "CHARITY_NAME": "財團法人台東基督教醫院",
                    "CHARITY_CODE": "299"
                },
                ...
            },
            ..."
        }
    },
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
