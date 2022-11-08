---
description: Learn how to retrieve the JSON schema for an order refund.
---

# Retrieving the JSON schema for an order refund

Retrieve the JSON schema for a refund associated with an order like this where you provide the customer's token:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'http://{host}/orders/{orderid}/refunds-available' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
A successful request returns a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "status": "string",
  "reason": "string",
  "comments": "string",
  "type": "string",
  "category": "string",
  "generationDate": "string",
  "generatedBy": "string",
  "origin": "string",
  "overrides": "string",
  "policy": "string",
  "currency": "string",
  "totalRefunded": {
    "value": 0,
    "formattedValue": "string"
  },
  "outstanding": {
    "value": 0,
    "formattedValue": "string"
  },
  "totalRequested": {
    "value": 0,
    "formattedValue": "string"
  },
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
      "product": {
        "externalId": "string",
        "companyId": "string",
        "id": "string",
        "siteId": "string"
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
            "formattedValue": "string"
          }
        }
      ]
    }
  ],
  "id": "string",
  "companyId": "string",
  "siteId": "string"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
