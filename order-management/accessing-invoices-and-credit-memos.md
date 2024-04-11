---
description: >-
  Learn how to access order invoices and credit memos and then share them with
  your customers
---

# Accessing invoices and credit memos

For some transactions, Digital River automatically generates [order invoice](accessing-invoices-and-credit-memos.md#order-invoices) and [credit memo](accessing-invoices-and-credit-memos.md#credit-memos) files that you can access and then share with your customers. To do this, you can implement nearly identical solutions.&#x20;

For testing purposes, we also provide you the ability to generate [mock order invoices and credit memos](accessing-invoices-and-credit-memos.md#mock-order-invoices-and-credit-memos).

To localize these files, set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`locale`](../integration-options/checkouts/creating-checkouts/designating-a-locale.md).&#x20;

## Order invoices

In transactions assigned one of the following [selling entities](../integration-options/checkouts/creating-checkouts/selling-entities.md), Digital River automatically generates an order invoice in PDF that you can share with customers:

* `Digital River, Inc.`
* `DR globalTech Inc.`
* `Digital River Ireland Ltd.`
* `Digital River UK`
* `DR Japan`

### How to access the invoice file

By [listening for the order invoice created event](accessing-invoices-and-credit-memos.md#listening-for-the-order-invoice-created-event) or by [retrieving the order](accessing-invoices-and-credit-memos.md#retrieving-the-invoice-file-identifier-from-the-order), you can get an invoice's file identifier and then use it to generate a shareable link.&#x20;

{% hint style="info" %}
You can also [download an invoice in Digital River Dashboard](../administration/dashboard/order-management/orders/downloading-an-invoice.md).
{% endhint %}

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `totalAmount` is `0`, then Digital River doesn't generate a customer invoice.&#x20;

#### Listening for the order invoice created event

You can be notified when the invoice is created by listening for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of [`order.invoice.created`](events-and-webhooks-1/events-1/event-types.md#order.invoice.created).&#x20;

The event's [`data.object`](events-and-webhooks-1/events-1/#event-data) contains an `id` and a `fileId`, both of which are identical and hold the invoice's [file](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) identifier. You can use either to [create a publicly accessible link](accessing-invoices-and-credit-memos.md#creating-a-publicly-accessible-link).

{% tabs %}
{% tab title="order.invoice.created" %}
```javascript
{
    "id": "c902f8aa-16fb-44ba-ba7b-f3c84061685a",
    "type": "order.invoice.created",
    "data": {
        "object": {
            "id": "6e5bf525-3907-40c5-86a9-f14ce4f33f35",
            "fileId": "6e5bf525-3907-40c5-86a9-f14ce4f33f35",
            "orderId": "188418250336",
            "customerId": "532736320336",
            "purpose": "customer_invoice",
            "invoiceURL": "https://api.digitalriver.com/files/6e5bf525-3907-40c5-86a9-f14ce4f33f35/content"
        }
    },
    "liveMode": false,
    "createdTime": "2021-04-28T02:04:13.591115Z",
    "versionIds": []
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In the event's `data.object`, the `invoiceURL` can only be accessed with your [confidential (secret) API key](../developer-resources/api-structure.md#confidential-keys) so you shouldn't share this link with your customers because they won't be able to access its content.
{% endhint %}

#### Retrieving the invoice file identifier from the order

To access the customer invoice file, you can also [retrieve the order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders).&#x20;

Once invoices are generated, Digital River populates the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `invoicePDFs[]`. If `invoicePDFs[]` doesn't exist, then the [file(s)](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) have yet to be created.&#x20;

Each element of this array contains a [file's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) unique `id` and `url`.&#x20;

You'll need to use `invoicePDFs[].id` to [create a publicly accessible link](accessing-invoices-and-credit-memos.md#creating-a-publicly-accessible-link).

{% hint style="warning" %}
In the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), the `invoicePDFs[].url` can only be accessed with your [confidential (secret) API key](../developer-resources/api-structure.md#confidential-keys) so you shouldn't share this link with your customers because they won't be able to access its content.
{% endhint %}

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "188418250336",
    ...
    "invoicePDFs": [
        {
            "id": "6e5bf525-3907-40c5-86a9-f14ce4f33f35",
            "url": "https://api.digitalriver.com/files/6e5bf525-3907-40c5-86a9-f14ce4f33f35/content",
            "liveMode": false
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

### Creating a publicly accessible link

To create a publicly accessible link to the invoice [file](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files), assign its identifier to `fileId` and send it in the body of a [`POST /file-links`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/FileLinks/operation/createFileLinks) request.&#x20;

The response contains a `url` that you can share with your customers by email, in their account management portals, or by another method of your choice.

## Credit memos

A credit memo is a document issued to customers notifying them of a reduction in the amount they owe.

### How to access the credit memo file

By [listening for the credit memo created event](accessing-invoices-and-credit-memos.md#listening-for-the-credit-memo-created-event) or by [retrieving the order](accessing-invoices-and-credit-memos.md#retrieving-the-credit-memo-file-identifier-from-the-order), you can get a credit memo's file identifier and then use it to generate a shareable link.

#### Listening for the credit memo created event

You can be notified when a credit memo is created by listening for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of [`order.credit_memo.created`](events-and-webhooks-1/events-1/event-types.md#order.credit\_memo.created).&#x20;

The event's [`data.object`](events-and-webhooks-1/events-1/#event-data) contains an `id` and a `fileId`, both of which are identical and hold the credit memo's [file](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) identifier. You can use either to [create a publicly accessible link](accessing-invoices-and-credit-memos.md#creating-a-publicly-accessible-link-1).

{% tabs %}
{% tab title="order.credit_memo.created" %}
```javascript
{
    "id": "d3786b5b-540b-4885-92a4-62f937d13f26",
    "type": "order.credit_memo.created",
    "data": {
        "object": {
            "id": "c233c10f-17e8-4799-a1ce-2469d042f29d",
            "fileId": "c233c10f-17e8-4799-a1ce-2469d042f29d",
            "orderId": "188466550336",
            "customerId": "532795950336",
            "purpose": "customer_credit_memo",
            "invoiceURL": "https://api.digitalriver.com/files/c233c10f-17e8-4799-a1ce-2469d042f29d/content"
        }
    },
    "liveMode": false,
    "createdTime": "2021-04-29T02:15:20.516626Z",
    "versionIds": []
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In the event's `data.object`, the `invoiceURL` can only be accessed with your [confidential (secret) API key](../developer-resources/api-structure.md#confidential-keys) so you shouldn't share this link with your customers because they won't be able to access its content.
{% endhint %}

#### Retrieving the credit memo file identifier from the order

To access a customer's credit memo file, you can also [retrieve the order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders).&#x20;

Once credit memos are generated, Digital River populates the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `creditMemoPDFs[]`. If `creditMemoPDFs[]` doesn't exist, then the [file(s)](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) have yet to be created.

Each element of this array contains a [file's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) unique `id` and `url`.

You'll need to use `creditMemoPDFs[].id` to [create a publicly accessible link](accessing-invoices-and-credit-memos.md#creating-a-publicly-accessible-link-1).

{% hint style="warning" %}
In the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), the `creditMemoPDFs[].url` can only be accessed with your [confidential (secret) API key](../developer-resources/api-structure.md#confidential-keys) so you shouldn't share this link with your customers because they won't be able to access its content.
{% endhint %}

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "188418250336",
    ...
    "creditMemoPDFs": [
        {
            "id": "fb50c8c2-8b32-4a3d-9947-dbdef12a5cdc",
            "url": "https://api.digitalriver.com/files/fb50c8c2-8b32-4a3d-9947-dbdef12a5cdc/content",
            "liveMode": false
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

### Creating a publicly accessible link

To create a publicly accessible link to a customer's credit memo [file](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files), assign its identifier to `fileId` and send it in the body of a [`POST /file-links`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/FileLinks/operation/createFileLinks) request.&#x20;

The response contains a `url` that you can share with your customers by email, in their account management portals, or by another method of your choice.

## Mock order invoices and credit memos

You can also generate order invoice and credit memo files in [test mode](../developer-resources/best-practices.md#test-mode). The process of accessing them is the same as in the production environment.

The following are example mock tax invoice and credit memo PDFs:

{% file src="../.gitbook/assets/vat-invoice.pdf" %}
Sample VAT invoice
{% endfile %}

{% file src="../.gitbook/assets/credit-memo.pdf" %}
Sample credit memo
{% endfile %}
