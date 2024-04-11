---
description: Learn how to get a list of payouts.
---

# Returning a list of payouts

## Setting the payout query parameters

| Parameter     | Optional/Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| createdTime   | Optional          | <p>A filter on the list based on the <strong>createdTime</strong> field. The value can be a string with an ISO-601 UTC format datetime, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>createdTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>createdTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>createdTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>createdTime</code> field is before or equal to this timestamp</li></ul> |
| endingBefore  | Optional          | A cursor for use in pagination. The `endingBefore` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects starting with `xyz`, your subsequent calls can include `endingBefore=xyz` to fetch the previous page of the list.                                                                                                                                                                                                                                                                                                                                                                       |
| startingAfter | Optional          | A cursor for use in pagination. The `startingAfter` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects ending with `xyz`, your subsequent calls can include `startingAfter=xyz` to fetch the next page of the list.                                                                                                                                                                                                                                                                                                                                                                           |
| limit         | Optional          | A limit on the number of objects returned. The limit can range between 1 and 100, and the default is 10.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ids           | Optional          | Only return objects with these identifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| payoutTime    | Optional          | <p>A filter on the list based on the payout <code>payoutTime</code> field. The value can be a string with an ISO-601 UTC format datetime or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>payoutTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>payoutTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>payoutTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>payoutTime</code> field is before or equal to this timestamp</li></ul>    |
| payerId       | Optional          | Only return payouts with this payer identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| payerName     | Optional          | Only return payouts with this payer name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| payeeId       | Optional          | Only return payouts with this payee identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| payeeName     | Optional          | Only return payouts with this payee name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| currency      | Optional          | Only return sales transactions in this currency.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| amount        | Optional          | <p>A filter on the list based on the payout <code>amount</code> field. The value can be a string or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>amount</code> field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>amount</code> field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>amount</code> field is less than this amount</li><li><strong>lte</strong>–return values where the <code>amount</code> field is less than or equal to this amount</li></ul>                                                    |

## Example get request and response

Retrieve the details of payouts with a `GET` request:

{% tabs %}
{% tab title="cURL" %}
```http
curl https://api.digitalriver.com/payouts
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns an array of [Payout ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Payouts)objects:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "hasMore": true,
  "data": [
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
  ]
}
```
{% endtab %}
{% endtabs %}

## Key payout attributes

The following information provides details on the key attributes returned in response to a request for [payout ](./)information. For a complete list, refer to the [Payouts API reference](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Payouts).

### id

A unique identifier for the payout.&#x20;

### createdTime

The time at which the payout was created in the reporting environment.

### payoutTime

The time when the payout was transacted.&#x20;

### currency

The three-letter ISO currency code representing the type of currency used in the payout.

### amount

Represents the total payout amount.&#x20;

### payerId

The ID of payer.&#x20;

### payerName

The name of the payer.

### payeeId

The ID of the payee.

### payeeName

The name of the payee.

### liveMode

If the value is True, the object exists in live mode. If the value is False, the object exists in test mode. Only live mode is supported.
