---
description: Learn how to return a list of sales summaries.
---

# Returning a list of sales summaries

## Setting sales summary query parameters

| Parameter        | Optional/Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| createdTime      | Optional          | <p>A filter on the list based on the <strong>createdTime</strong> field. The value can be a string with an ISO-601 UTC format datetime, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>createdTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>createdTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>createdTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>createdTime</code> field is before or equal to this timestamp</li></ul>                                    |
| endingBefore     | Optional          | A cursor for use in pagination. The `endingBefore` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects starting with `xyz`, your subsequent calls can include `endingBefore=xyz` to fetch the previous page of the list.                                                                                                                                                                                                                                                                                                                                                                                                          |
| startingAfter    | Optional          | A cursor for use in pagination. The `startingAfter` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects ending with `xyz`, your subsequent calls can include `startingAfter=xyz` to fetch the next page of the list.                                                                                                                                                                                                                                                                                                                                                                                                              |
| limit            | Optional          | A limit on the number of objects returned. The limit can range between 1 and 100, and the default is 10.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ids              | Optional          | Only return objects with these identifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| salesClosingTime | Optional          | <p>A filter on the list based on the sales summary <code>salesClosingTime</code> field. The value can be a string with an ISO-601 UTC format datetime, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>salesClosingTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>salesClosingTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>salesClosingTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>salesClosingTime</code> field is before or equal to this timestamp</li></ul> |
| paid             | Optional          | Only return sales summaries that have been paid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| payoutId         | Optional          | Only return sales summaries with this payout identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| currency         | Optional          | Only return sales summaries in this currency.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| amount           | Optional          | <p>A filter on the list based on the sales summaries<code>amount</code> field. The value can be a string or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>amount</code> field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>amount</code> field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>amount</code> field is less than this amount</li><li><strong>lte</strong>–return values where the <code>amount</code> field is less than or equal to this amount</li></ul>                                                                               |
| payerId          | Optional          | Only return sales summaries with this payer identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| payerName        | Optional          | Only return sales summaries with this payer name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| payeeId          | Optional          | Only return sales summaries with this payee identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| payeeName        | Optional          | Only return sales summaries with this payee name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## **Example get request and response**

Retrieve the details of sales summaries with a `GET` request:

{% tabs %}
{% tab title="cURL" %}
```http
curl https://api.digitalriver.com/sales-summaries
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns an array of [Sales Summary](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-summaries) objects:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "hasMore": true,
  "data": [
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
  ]
}
```
{% endtab %}
{% endtabs %}

## Key sales summaries attributes

The following information provides details on the key attributes returned in response to a request for [sales summaries](../../administration/dashboard/finance/sales-summaries/) information. For a complete list, refer to the [Sales summaries API reference](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-summaries).

### id

A unique identifier for the sales summary.&#x20;

### createdTime

The time at which the sales summary was created in the reporting environment&#x20;

### salesClosingTime

The end date of that sales summary time frame as defined in the reporting environment.

### currency

The three-letter ISO currency code representing the currency used in sales summary reporting.&#x20;

### amount

Represents the total sales summary amount reported in the requested currency.&#x20;

### payoutTransactionId

A unique identifier for a payout associated with the specific sales summary. Sales summaries are initially created without a `payoutId`. The value is updated when the sales summary is paid.

### payoutId

A unique identifier for a payout associated with the specific sales summary. Sales summaries are initially created without a `payoutId`. The value is updated when the sales summary is paid..

### paid

If the value is True, it indicates that this sales summary has been paid. This value is useful for creating a filter in choosing data for a report.

### payerId

The ID of payer.&#x20;

### payerName

The name of the payer.

### payeeId

The ID of the payee.

### liveMode

If the value is True, the object exists in live mode. If the value is False, the object exists in a test mode. Only live mode is supported.
