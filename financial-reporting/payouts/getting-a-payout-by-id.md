---
description: Learn how to get a payout by identifier.
---

# Getting a payout by ID

## Setting payout path parameters

The following table lists the required parameters you can provide in a [get payout by ID](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrievePayouts) request.

| Parameter | Required/Optional | Description               |
| --------- | ----------------- | ------------------------- |
| id        | Required          | Unique payout identifier. |

## **Example get request and response**

To retrieve details of a payout, you must supply the unique identifier of the payout:

{% tabs %}
{% tab title="Request header example" %}
```http
GET /payouts​/2000028600_1410_2019
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns the Payout object.

{% tabs %}
{% tab title="Payout object" %}
```javascript
{
  "id": "2000028600_1410_2019",
  "createdTime": "2019-04-25T20:36:00Z",
  "payoutTime": "2019-04-25T00:00:00Z",
  "currency": "USD",
  "amount": 1180.26,
  "payerId": "1410",
  "payerName": "DR globalTech, Inc.",
  "payeeId": "0013900100",
  "payeeName": "ACME, Inc.",
  "liveMode": true
}
```
{% endtab %}
{% endtabs %}
