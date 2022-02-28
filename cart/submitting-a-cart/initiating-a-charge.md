---
description: Learn how to specify the type of charge.
---

# Initiating a charge

When you [create](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) or [update](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) a Cart, the Commerce API calculates the `chargeType` based on the information set up in Global Commerce. You can use the `chargeType` parameter to tell Digital River whether you expect the [payment source](../sources/) to be used for a [customer-initiated](initiating-a-charge.md#customer-initiated), [merchant-initiated](initiating-a-charge.md#merchant-initiated), or [mail/telephone-initiated](initiating-a-charge.md#mail-order-telephone-order) transaction.&#x20;

{% tabs %}
{% tab title="cURL" %}
```http
curl --location --request POST 'http://<<host>>/v1/shoppers/me/carts/active' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "cart": {
    "lineItems": {
      "lineItem": {
        "quantity": "2",
        "product": {
          "id": 1234
        }
      }
    },
    "chargeType": "moto"
  }
}'
```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response. The response shows the `chargeType` in the order level.&#x20;

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "order": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278080023",
    "id": "47278080023",
    "submissionDate": "2018-04-27T20:31:13.109Z",
    "displayName": "New Order",
    "locale": "en_US",
    "optIn": "false",
    "testOrder": "false",
    "taxExempt": "false",
    "businessEntityCode": "DR_INC-ENTITY",
    "orderState": "Submitted",
    "orderStateDetails": {
      "description": "Settled",
      "settled": {
        "currency": "USD",
        "value": "19.99"
      },
      "refunded": {
        "currency": "USD",
        "value": "19.99"
      }
    "chargeType": "moto"    
    },
    "customAttributes": {
      "attribute": [
        {
          "name": "name",
          "value": "string",
          "type": "string"
        }
      ]
    }
  },
```
{% endtab %}
{% endtabs %}

## Customer initiated

In this case, the cardholder actively participates in the transaction. A `customer-initiated` transaction is the most common charge type, representing the majority of online checkouts or invoices. During these transactions, the [customer provides payment details](../sources/retrieving-sources.md) when they submit the cart or uses [stored payment information](../sources/retrieving-sources.md). &#x20;

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| Yes                | Yes                       |

## Merchant initiated

A `merchant_initiated`  transaction is submitted using stored payment details without the cardholder's active participation during the checkout or invoice process. This charge type can only occur when an agreement exists that allows the client to initiate payments on behalf of their customers.&#x20;

Since Digital River acts as the [authorized reseller of record](../../#working-with-digital-river), we initiate and process the transaction on your behalf. You, in turn, are acting on the behalf of your customer.

[Subscription renewals](../sources/retrieving-sources.md) and automated payments for water, sewer, gas, or electric utilities are common examples of this charge type.

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| No                 | No                        |

## Mail order/telephone order

A Mail Order/Telephone Order (MOTO) is a payment card transaction initiated by mail, fax, or over the phone.  In these `moto` transactions, customers provide you their payment details by regular mail, fax, or telephone. By passing this information to you, the customer authorizes you (who, in turn, authorizes Digital River) to process the transaction.&#x20;

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| Yes                | No                        |
