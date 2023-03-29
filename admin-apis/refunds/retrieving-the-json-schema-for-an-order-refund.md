---
description: Learn how to retrieve the JSON schema for an order refund.
---

# Getting the JSON schema for an order refund

Use the [`GET /orders/{orderId}/refunds/schema`](https://drapi.io/commerce/test/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds\~1schema/get) to retrieve the JSON schema for a refund associated with an order.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/{orderid}/refunds/schema' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
A successful request returns a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "status": "string",
  "reason": "CUSTOMER_SATISFACTION_ISSUE",
  "comments": "string",
  "type": "PRODUCT_SHOULD_NOT_HAVE_FEE",
  "category": "PRODUCT_LEVEL_FEE",
  "generationDate": "string",
  "origin": "string",
  "overrides": "string",
  "policy": "string",
  "currency": "string",
  "totalRefunded": {},
  "outstanding": {},
  "totalRequested": {},
  "refundAmount": {
    "value": 0,
    "formattedValue": "string"
  },
  "lineItems": [
    {
      "status": "string",
      "expectedQuantity": 0,
      "returnedQuantity": 0,
      "type": "string",
      "notes": "string",
      "date": "string",
      "Product": {
        "companyId": "string",
        "id": "string",
        "externalId": "string"
      },
      "lineItemId": "string",
      "refundAmount": {
        "value": 0,
        "formattedValue": "string"
      },
      "lineItemFees": [
        {
          "feeType": "string",
          "refundAmount": {
            "value": 0,
            "currency": "string"
          }
        }
      ]
    }
  ],
  "id": "string",
  "companyId": "string",
  "siteId": "string",
  "generatedBy": "string"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
