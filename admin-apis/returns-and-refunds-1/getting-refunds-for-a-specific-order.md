---
description: Learn how to get refunds for a specific order.
---

# Getting refunds for a specific order

Use [`GET /orders/{orderId}/refunds`](https://drapi.io/commerce/test/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds/get) request with the order identifier (`orderId`) to get refunds for a specific order.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/{orderid}/refunds' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "refunds": [
    {
      "id": "string",
      "status": "string",
      "reason": "string",
      "comments": "string",
      "type": "string",
      "category": "string",
      "generationDate": "string",
      "generatedBy": "string",
      "origin": "string",
      "policy": "string",
      "currency": "string",
      "totalRefunded": {},
      "outstanding": {},
      "totalRequested": {}
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
