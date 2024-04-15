---
description: Learn how to specify the type of charge.
---

# Initiating a charge

When [creating](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [updating](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) a Checkout or [creating ](../subscriptions/invoices.md#creating-an-invoice)an Invoice, you can use the `chargeType` parameter to tell Digital River whether you expect the [payment source](../../../payments/payment-sources/) to be used for a [customer-initiated](initiating-a-charge.md#customer-initiated), [merchant-initiated](initiating-a-charge.md#merchant-initiated), or [mail/telephone-initiated](initiating-a-charge.md#mail-order-telephone-order) transaction.

## Customer initiated

In this case, the cardholder actively participates in the transaction. A `customer-initiated` transaction is the most common charge type, representing the majority of online checkouts or invoices. During these transactions, the [customer provides payment details](../../../payments/payment-sources/using-the-source-identifier.md#charging-a-single-use-source) at the time of checkout or invoice or uses [stored payment information](../../../payments/payment-sources/using-the-source-identifier.md#attaching-a-source-to-a-customer).

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| Yes                | Yes                       |

## Merchant initiated

A `merchant_initiated` transaction is submitted using stored payment details without the cardholder's active participation during the checkout or invoice process. This charge type can only occur when an agreement exists that allows the client to initiate payments on behalf of their customers.

Since Digital River acts as the [authorized reseller of record](../../../), we initiate and process the transaction on your behalf. You, in turn, are acting on the behalf of your customer.

[Subscription renewals](../subscriptions/subscription-information-1.md#creating-and-renewing-subscriptions) and automated payments for water, sewer, gas, or electric utilities are common examples of this charge type.

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| No                 | No                        |

## Mail order/telephone order

A Mail Order/Telephone Order (MOTO) is a payment card transaction initiated by mail, fax or over the phone. In these `moto` transactions, customers provide the merchant their payment details by regular mail, fax, or telephone. By supplying this information, the customer authorizes the merchant (who, in turn, authorizes Digital River) to process the transaction.

Additionally, when `chargeType` is set to `moto`, the user is only presented with payment methods that support this type of transaction. This is true whether your integration displays payment methods using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).&#x20;

| Can a CVV be used? | Can 3DS measures be used? |
| ------------------ | ------------------------- |
| Yes                | No                        |
