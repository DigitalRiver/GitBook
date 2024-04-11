---
description: Learn how to get a sales transaction by identifier.
---

# Getting a sales transaction by ID

## Setting sales transaction path parameter

The following table lists the required parameters you can provide in a [get Sales Transactions by ID](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSalesTransactions) request.

| Parameter | Required/Optional | Description                          |
| --------- | ----------------- | ------------------------------------ |
| `id`      | Required          | Unique sales transaction identifier. |

## Example get request and response

To retrieve details of a sales transaction, you must supply the unique identifier of the sales transaction with the `GET` request:

{% tabs %}
{% tab title="cURL" %}
```
curl https://api.digitalriver.com/sales-transactions/0206802584_000010_3700005504
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns the [Sales Transaction](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-transactions) object:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "id": "0206802584_000010_3700005504",
  "createdTime": "2019-04-25T20:36:00Z",
  "saleTime": "2019-04-25T00:00:00Z",
  "salesSummaryId": "8100000400_1410_2019",
  "currency": "GBP",
  "amount": 443.08,
  "type": "sale",
  "orderId": "37031462099",
  "skuId": "945-0198",
  "quantity": 1,
  "payoutAmounts": {
    "currency": "USD",
    "exchangeRate": 1.24535,
    "amount": 551.79,
    "tax": -91.97,
    "shipping": -14.36,
    "regulatoryFees": 0,
    "landedCost": 0,
    "productPrice": 445.46,
    "digitalRiverShare": -41.38,
    "distributorShare": -375.61,
    "transactionFees": 0,
    "shippingDiscount": 0,
    "regulatoryFeeDiscount": 0,
    "remitShipping": 0,
    "payoutAmount": 28.47,
    "storeCredit": 0.0
   }, 
    "payerId": "1410",
    "payerName": "DR globalTech, Inc.",
    "payeeId": "0000000000",
    "payeeName": "ACME, Inc.",
    "liveMode": true,
    "orderUpstreamId": "923456789",
    "skuTaxCode": "601410",
    "shipFromCountry": "US",
    "shipToCountry": "US",
    "billToCountry": "US",
    "paymentType": "creditCard",
    "lineItemId": "2221136454639",
    "orderMetadata": {

    },
    "lineItemMetadata": {  
}
```
{% endtab %}
{% endtabs %}
