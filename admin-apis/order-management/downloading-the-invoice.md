---
description: Learn how to download the invoice PDF file for an order.
---

# Downloading the invoice

An invoice represents a document associated with a sale you provide to the shopper. The invoice itemizes the products or services rendered and includes their cost, quantity, fees, duties, and taxes. It also establishes an obligation on the part of the shopper to pay you for those products and services.

Invoices can be especially useful when selling to other businesses. For business transactions, it's often customary to send customers an invoice, which they pay at a later time, rather than immediately billing a credit card you have on file.

This topic explains how to download the invoice PDF file.

## Invoice PDF download scenarios

You can [download the invoice PDF programmatically](downloading-the-invoice.md#downloading-the-invoice-pdf-programmatically) or [from a webhook notification](downloading-the-invoice.md#downloading-the-invoice-pdf-via-a-webhook-notification).

### Downloading the invoice PDF programmatically

To download the invoice PDF programmatically:

1. [Get the download information for the order's invoice](downloading-the-invoice.md#step-1-getting-the-download-information-for-the-orders-invoice).
2. [Get the receipt for the order's invoice](downloading-the-invoice.md#step-2-getting-the-receipt-for-the-invoice) and download the PDF in the `200 OK` response.

#### Step 1: Getting the download information for the order's invoice

Use the [`GET /v1/orders/{orderId}/invoices`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Invoice/paths/\~1v1\~1orders\~1%7BorderId%7D\~1invoices/get) request to get the specified orders (`orderId`) invoice download information. An order may contain more than one invoice (`invoiceUrl`). This request includes all downloadable invoice URLs (`invoiceURL`) in the response. You can [use the receipt identifier (`receiptId`) to download the invoices one by one](downloading-the-invoice.md#step-3-getting-the-receipt-for-the-invoice).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/orders/{orderId}/invoices' \
--header 'authorization: basic ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```
{
    "invoices": [
        {
            "type": "vat_invoice",
            "invoiceURL": "https://dispatch-test.digitalriver.com/v1/orders/1075294270082/invoices/{receiptId}"
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 2: Getting the receipt for the invoice

Use the [`GET /v1/orders{orderId}/invoices/{receiptId}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Invoice/paths/\~1v1\~1orders\~1%7BorderId%7D\~1invoices\~1%7BreceiptId%7D/get) request to download the invoice by its invoice identifier (`receiptId`) for a specific order (`orderId`).&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/orders/{orderId}/invoices/{receiptId}' \
--header 'authorization: basic ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will get a `200 OK` response with the PDF file.

<figure><img src="../../.gitbook/assets/Order invoice.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

### Downloading the invoice PDF via a webhook notification

{% hint style="success" %}
You must [enable the following events when creating a webhook](https://help.digitalriver.com/help/gc/Administration/Webhook-Service/Webhook-service.htm#createWebhook) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) before you can perform this task:

* `order.invoice.created`: The creation of an order invoice triggers this event.
{% endhint %}

To download the invoice PDF from an invoice URL:

1. [Get the file identifier for the invoice](downloading-the-invoice.md#step-1-getting-the-file-identifier-for-the-invoice).
2. [Get the invoice PDF file](downloading-the-invoice.md#step-2-getting-the-invoice-pdf-file).

#### Step 1: Getting the file identifier for the invoice

When the invoice file is created, it triggers the `order.invoice.created` event and you will receive a notification. Choose one of the following options:

* Copy the value for the `fileId`. You will need that value to [get the invoice PDF file](downloading-the-invoice.md#step-2-getting-the-invoice-pdf-file).
* Copy the value for the invoice URL and paste it into your browser's address field.

{% code overflow="wrap" %}
```json
{
    "id": "db375d32-52c0-4188-a05c-552933d254c5",
    "type": "order.invoice.created",
    "data": {
        "object": {
            "id": "9e00869b-e2f5-4663-aacb-e33687466020",
            "fileId": "9e00869b-e2f5-4663-aacb-e33687466020",
            "orderId": "851511800082",
            "customerId": "503451273389",
            "purpose": "customer_invoice",
            "invoiceURL": "https://api.digitalriver.com/files/9e00869b-e2f5-4663-aacb-e33687466020/content"
        }
    },
    "liveMode": false,
    "createdTime": "2020-10-14T09:03:33.988Z"
}
```
{% endcode %}

#### Step 2: Getting the invoice PDF file

Use the  [`GET /files/{fileId}/content`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-File/operation/downloadFiles) request to fetch the invoice PDF file specified by the file identifier (`fileId`) provided in the notification.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/files/{fileId}/content' \
--header 'authorization: basic***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
<pre class="language-json" data-overflow="wrap"><code class="lang-json"><strong>{
</strong>  "id": "9e00869b-e2f5-4663-aacb-e33687466020",
  "fileName": "File Name"
}
</code></pre>
{% endtab %}
{% endtabs %}
