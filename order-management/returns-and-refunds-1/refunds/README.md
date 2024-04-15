---
description: Learn the basics of issuing refunds
---

# Refund basics

A smooth, easy to use refund process can provide your customers a positive experience. Being able to deliver timely refunds can also help minimize your risk of [chargebacks](../disputes-and-chargebacks.md).

The [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) allows you to issue customers full or partial refunds on product costs, shipping expenses, taxes, duties, and fees. The API also gives you the ability to refund the same [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) multiple times. You cannot however [issue a refund](issuing-refunds.md) that's greater than the combined amount of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [charges](../../orders/payment-charges/).

You can also [create refunds manually](../../../administration/dashboard/order-management/orders/creating-a-refund.md) through [Digital River Dashboard](../../../administration/dashboard/).

## Where refunds are sent

Refunds can only be applied to the payment method that was used to make the purchase.

{% hint style="success" %}
For details on how we refund purchases made with multiple payment methods, refer to [How we handle captures, cancels, and refunds](../../../payments/payment-sources/using-the-source-identifier.md#how-we-handle-captures-cancels-and-refunds) when [Combining primary and secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md) page.
{% endhint %}

If customers used a credit card to make the purchase, and that card is cancelled or expires prior to your refund request, then most of the time card issuers can still handle the refund. Typically, the issuer credits the customer's replacement card but, in situations where no replacement exists, a check is usually mailed.

## Tracking a refund

After you [submit a refund request](issuing-refunds.md), Digital River relays your request to the customer's bank or credit card issuer. If the request is approved, your integration typically receives the [`refund.complete`](issuing-refunds.md#completed-refunds) event within 24 hours. However, it may take five to ten business days before customers see the credit on their statements.

## Dealing with refund failures

In the unlikely event that a [refund request](issuing-refunds.md) fails, the [refund's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) `state` transitions to `failed` . You can be notified of this state change by subscribing to the [`refund.failed`](issuing-refunds.md#failed-refunds) event. When Digital River is able to pinpoint the cause of the failure, `failureReason` is populated in the event's payload.

## Notifying customers of successful refunds

When a refund request is approved, the refund's `state` transitions to `succeeded` . You can be notified of this state change by subscribing to the [`refund.complete`](issuing-refunds.md#completed-refunds) event. We recommend you wait to receive this event before informing customers that their refund was successfully processed.
