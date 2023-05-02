---
description: Understand the refund credit memo event.
---

# Refund credit memo event

The creation of a refund credit memo (`order.credit_memo.created`) triggers this event. The refund credit memo file is created after a refund. The webhook response contains the invoice URL (`invoiceUrl`). See [Downloading the invoice PDF via a webhook notification](../../../admin-apis/order-management/downloading-the-invoice.md#downloading-the-invoice-pdf-via-a-webhook-notification) for more information to download the file.

{% code title="Webhook response" overflow="wrap" %}
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
