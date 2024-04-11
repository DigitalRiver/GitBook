---
description: Learn how to get a list of transactions included in the payout by identifier.
---

# Get a list of transactions included in payout by ID

## Setting payout path parameters

The following table lists the required parameters you can provide in a [get payout by ID](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrievePayouts) request.

| Parameter | Required/Optional | Description               |
| --------- | ----------------- | ------------------------- |
| id        | Required          | Unique payout identifier. |

## **Example get request and response**

To retrieve a list of transactions for a payout, you must supply the unique identifier of the payout:

{% tabs %}
{% tab title="Request header example" %}
```http
GET /payouts/8100000400_1410_2019/transactions
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns an array of Payout Transaction objects.

{% tabs %}
{% tab title="Payout Transaction object example" %}
```javascript
{
  "hasMore": true,
  "data": [
    {
      "id": "8100000400_1410_2019",
      "createdTime": "2018-04-25T20:36:00Z",
      "currency": "USD",
      "amount": 1180.26,
      "payoutId": "2000028600_1410_2019",
      "description": "Sales for Period Ended 04-25-2020",
      "type": "sales_summary",
      "liveMode": true
    }
  ]
}
```
{% endtab %}
{% endtabs %}

## Key payout transaction attributes

The following information provides details on the key attributes returned in response to a request for payout transaction information. For a complete list, refer to the [Payouts API reference.](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Payouts/operation/retrievePayouts)

### id

A unique identifier for the payout transaction.&#x20;

### createdTime

The time at which the payout transaction was created in the reporting environment.

### currency

The three-letter ISO currency code representing the type of currency used in the payout transaction.

### amount

Represents the payout transaction amount.&#x20;

### payoutId

The unique payout identifier.&#x20;

### salesSummaryId&#x20;

A unique identifier for the  sales summary containing the payout transactions.

### description

A text description of the payout transaction.&#x20;

### type

Designates the type of payout transaction. Supported types are `sale`, `return`, `refund`, `fraud_chargeback`, and `non_fraud_chargeback`.
