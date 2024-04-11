---
description: Learn how to get a list of sales transactions.
---

# Returning a list of sales transactions

## Setting the sales transaction query parameters

| Parameter           | Optional/Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `createdTime`       | Optional          | <p>A filter on the list based on the <strong>createdTime</strong> field. The value can be a string with an ISO-601 UTC format datetime, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>createdTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>createdTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>createdTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>createdTime</code> field is before or equal to this timestamp</li></ul>             |
| `endingBefore`      | Optional          | A cursor for use in pagination. The `endingBefore` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects starting with `xyz`, your subsequent calls can include `endingBefore=xyz` to fetch the previous page of the list.                                                                                                                                                                                                                                                                                                                                                                                   |
| `startingAfter`     | Optional          | A cursor for use in pagination. The `startingAfter` parameter is an object identifier that defines your place in the list. For instance, if you make a list request and receive 100 objects ending with `xyz`, your subsequent calls can include `startingAfter=xyz` to fetch the next page of the list.                                                                                                                                                                                                                                                                                                                                                                                       |
| `limit`             | Optional          | A limit on the number of objects returned. The limit can range between 1 and 100, and the default is 10.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `ids`               | Optional          | Only return objects with these identifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `saleTime`          | Optional          | <p>A filter on the list based on the sales transaction <code>saleTime</code> field. The value can be a string with an ISO-601 UTC format datetime or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>saleTime</code> field is after this timestamp</li><li><strong>gte</strong>–return values where the <code>saleTime</code> field is after or equal to this timestamp</li><li><strong>lt</strong>–return values where the <code>saleTime</code> field is before this timestamp</li><li><strong>lte</strong>–return values where the <code>saleTime</code> field is before or equal to this timestamp</li></ul>               |
| `salesSummaryId`    |                   | Only return sales transactions with this sales summary identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `type`              | Optional          | Only return sales transactions of this type. The enum are `sale, replacement, replacement_refund`, `replacement`, `replacement_return`, `fraud_chargeback`, `non_fraud_chargeback`, `refund`, `return`, `fraud_detection`, or `declined_settlement`.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `currency`          | Optional          | Only return sales transactions in this currency.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `orderId`           | Optional          | Only return sales transactions with this order identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `skuId`             | Optional          | Only return sales transactions with this SKU identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `quantity`          | Optional          | <p>A filter on the list based on the sales transaction <code>quantity</code> field. The value can be a string or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>quantity</code> field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>quantity</code> field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>quantity</code> field is less than this amount</li><li><strong>lte</strong>–return values where the <code>quantity</code> field is less than or equal to this amount</li></ul>                                           |
| `amount`            | Optional          | <p>A filter on the list based on the sales transaction <code>amount</code> field. The value can be a string or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>amount</code> field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>amount</code> field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>amount</code> field is less than this amount</li><li><strong>lte</strong>–return values where the <code>amount</code> field is less than or equal to this amount</li></ul>                                                     |
| `digitalRiverShare` | Optional          | <p>A filter on the list based on the sales transaction <code>digitalRiverShare</code> field. The value can be a string, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>digitalRiverShare</code>field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>digitalRiverShare</code>field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>digitalRiverShare</code>field is less than this amount</li><li><strong>lte</strong>–return values where the <code>digitalRiverShare</code>field is less than or equal to this amount</li></ul> |
| `payoutAmount`      | Optional          | <p>A filter on the list based on the sales transaction <code>payoutAmount</code> field. The value can be a string, or it can be a dictionary with the following options:</p><ul><li><strong>gt</strong>–return values where the <code>payoutAmount</code> field is greater than this amount</li><li><strong>gte</strong>–return values where the <code>payoutAmount</code> field is greater than or equal to this amount</li><li><strong>lt</strong>–return values where the <code>payoutAmount</code> field is less than this amount</li><li><strong>lte</strong>–return values where the <code>payoutAmount</code> field is less than or equal to this amount</li></ul>                      |

## Example get request and response

Retrieve the details of sales transactions with a `GET` request:

{% tabs %}
{% tab title="cURL" %}
```http
curl https://api.digitalriver.com/sales-transactions
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns an array of [Sales Transaction](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-transactions) objects:

{% tabs %}
{% tab title="JSON" %}
<pre class="language-javascript"><code class="lang-javascript">{
  "hasMore": true,
  "data": [
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
        "payoutAmount": 28.47
      },
      "payerId": "1410",
      "payerName": "DR globalTech, Inc.",
      "payeeId": "0013900100",
      "payeeName": "ACME, Inc.",
      "liveMode": true
      "orderMetadata": {
<strong>          "coupon": "iOS"
</strong><strong>      },
</strong><strong>      "lineItemMetadata": {
</strong>          "coupon": "iOS"
      }
  ]
}
</code></pre>
{% endtab %}
{% endtabs %}

## Key sales transaction attributes

The following information provides you with details on the key attributes returned in response to a request for a [sales transaction](./) information. For a complete details, refer to the [Sales transactions API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-transactions) reference.

### id

A unique identifier for a sales transaction. A sales transaction can be defined as a fulfilled sales order line. \
\
Sales transactions are created at the fulfillment level. As an example, let's say you have an order with line item 1 one and line item 2. If you just fulfill line item 1, you'll see a single sales transaction. If you fulfill only half of the quantity of line item 2, you'll see another sales transaction created. When you finally fulfill the other half of the quantity of line 2, you will see a third new sales transaction.

### createdTime

The time at which the sales transaction was created in the reporting environment.

### saleTime

The time when the order line item was fulfilled. Sales transactions are handled at the fulfillment level. As an example, let's say you have an order with line item 1 and line item 2. If you just fulfill line item 1, you'll see a single sales transaction. If you fulfill only half of the quantity of line item 2, you'll see another sales transaction created. When you finally fulfill the other half of the quantity of line 2, you will again see a new sales transaction.

### salesSummaryId

A unique identifier for a sales summary associated with the specific sales transaction. Sales transactions are initially created without a `salesSummaryId`. This value is updated when the sales transaction is grouped with other sales transactions into a sales summary.

### orderUpstreamId

A unique identifier generated by the upstream application or commerce platform.

### currency

The three-letter ISO currency code representing the type of currency used in the sales transaction.

### amount

The sales transaction total amount in the customer's currency. This amount multiplied by the `payoutAmounts.exchangeRate` (see below) gives you the `payoutAmounts.amount` in the requested payout currency.

### type

Designates the type of transaction. Supported types are `sale`, `return`, `refund`, `fraud_chargeback`, and `non_fraud_chargeback`.

### orderId

A unique identifier for the order.

### skuId

A unique identifier for the SKU.

### quantity

The quantity fulfilled for that SKU.

### payoutAmounts.

This section of returned data describes all information related to the [payout amount](../payouts/) of a sales transaction. For example, in the [payout process](../../administration/dashboard/finance/payouts/) you might sell something in Norwegian kroner but in the payout step of the sales transaction, it would be converted to U.S. dollars if that is the requested payout currency.

### payoutAmounts.currency&#x20;

The three-letter ISO currency code representing the type of currency to be used in the sales transaction payout.

### payoutAmounts.exchangeRate

The exchange rate used convert the sales amount from the sales order currency into the payout currency. The`amount` (above) multiplied by the `payoutAmounts.exchangeRate` (see below) gives you the `payoutAmounts.amount`.

### payoutAmounts.amount

The amount charged to the shopper for the fulfilled line item. The `amount`(see above) multiplied by the `payoutAmounts.exchangeRate` (see below) gives you the `payoutAmounts.amount`.

### payoutAmounts.tax&#x20;

The sales transaction tax amount in the currency used for the payout. The `payoutAmounts.amount` minus the payout tax, shipping, regulatory fees, and landed costs gets you the`payoutAmounts.productPrice`.

### payoutAmounts.shipping&#x20;

The sales transaction shipping amount in the currency used for the payout. The `payoutAmounts.amount` minus payout tax, shipping, regulatory fees, and landed costs gets you the`payoutAmounts.productPrice`.

### payoutAmounts.regulatoryFees&#x20;

The regulatory fees amount in the currency used for the payout. The `payoutAmounts.amount`  minus payout tax, shipping, regulatory fees, and landed costs gets you the`payoutAmounts.productPrice`.

### payoutAmounts.landedCost&#x20;

The [landed costs](../../integration-options/checkouts/creating-checkouts/landed-costs.md#what-is-landed-cost) amount. The `payoutAmounts.amount`minus payout tax, shipping, regulatory fees, and landed costs gets you the `payoutAmounts.productPrice`.

### payoutAmounts.productPrice&#x20;

The product price that does not include any taxes or fees. The `payoutAmounts.amount` minus payout tax, shipping, regulatory fees, and landed costs gets you the `payoutAmounts.productPrice`.

### payoutAmounts.digitalRiverShare&#x20;

The margin that Digital River receives for services. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount, and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.&#x20;

### payoutAmounts.distributorShare

The distributor share amount. This is always a value of "0."

### payoutAmounts.transactionFees

The transaction fees amount. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount, and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.&#x20;

### payoutAmounts.shippingDiscount&#x20;

The shipping discount amount. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.

### payoutAmounts.regulatoryFeeDiscount

The regulatory fee discount amount. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount, and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.

### payoutAmounts.remitShipping&#x20;

The shipping remittance amount. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount, and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.

### payoutAmounts.payoutAmount&#x20;

Total payout amount. The `payoutAmounts.productPrice` plus or minus the Digital River share, transaction fees, shipping discount, regulatory fee discount, and the shipping remittance amount gets you the total payout amount `payoutAmounts.payoutAmount`.

### payerId

The ID of payer.&#x20;

### payerName

The name of the payer&#x20;

### payeeId

The ID of the payee.&#x20;

### payeeName

The name of the payee.&#x20;

### liveMode

If the value is True, the object exists in live mode. If the value is False, the object exists in test mode. Only live mode is supported.

### orderMetadata

Key-value pairs used to store additional order level data. The value can be string, boolean, or integer types.

### lineItemMetadata

Key-value pairs used to store additional line-item level data. The value can be string, boolean, or integer types.
