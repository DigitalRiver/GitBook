---
description: Learn how to get a sales summary by identifier.
---

# Getting a sales summary by ID

## Setting sales summary path parameter

The following table lists the required parameters you can provide in a [get Sales Summary by ID](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSalesSummaries) request.

| Parameter | Required/Optional | Description                      |
| --------- | ----------------- | -------------------------------- |
| id        | Required          | Unique sales summary identifier. |

## **Example get request and response**

To retrieve details of a sales summary, you must supply the unique identifier of the sales summary:

{% tabs %}
{% tab title="Request header example" %}
```http
curl https://api.digitalriver.com/sales-summaries/8100000400_1410_2019
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns the [Sales Summary](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-summaries) object.

{% tabs %}
{% tab title="Sales Summary object example" %}
```javascript
{
  "id": "8100000400_1410_2019",
  "createdTime": "2019-04-25T20:36:00Z",
  "salesClosingTime": "2019-04-25T00:00:00Z",
  "currency": "USD",
  "amount": 1180.26,
  "payoutId": "2000028600_1410_2019",
  "paid": true,
  "payerId": "1410",
  "payerName": "DR globalTech, Inc.",
  "payeeId": "0013900100",
  "payeeName": "ACME, Inc.",
  "liveMode": true
}
```
{% endtab %}
{% endtabs %}
