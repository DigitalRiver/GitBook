---
description: Understand the invoice created event.
---

# Invoice created event

The creation of an order invoice (`order.invoice.created`) triggers this event. See [Getting the file identifier for the invoice](../../../admin-apis/order-management/downloading-the-invoice.md#step-1-getting-the-file-identifier-for-the-invoice) for more information.

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
