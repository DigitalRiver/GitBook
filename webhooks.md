---
description: Learn what webhooks are enabled with Digital River configuration.
---

# Webhooks

The webhooks listed below become automatically enabled once registration with Digital River is completed, and configure the Digital River **** app for your store.

{% hint style="info" %}
Each time you click **Save** on the [Payment Methods page](configure-the-bigCommerce-settings/step-2-configure-payments.md) in BigCommerce, BigCommerce automatically [creates a new webhook endpoint](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/webhooks/creating-a-webhook) within your Digital River account  You are responsible for [deleting any duplicate or old webhook endpoints](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/webhooks/deleting-a-webhook) within Digital River to avoid sending duplicate event data to BigCommerce.
{% endhint %}

| Webhook                         | Description                                                                                                                                                                                                      |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `order.accepted`                | When BigCommerce receives this webhook from Digital River, the payment status **** on the order in BigCommerce moves to authorized, **** and the order status moves to **** awaiting payment.                    |
| `order.blocked`                 | When BigCommerce receives this webhook, BigCommerce will move the payment status to declined, orders status to declined, and fraud status to rejected.                                                           |
| `order.charge.cancel.complete`  | When BigCommerce receives this webhook, BigCommerce will move payment status to void, and order status to cancelled.                                                                                             |
| `order.charge.capture.complete` | When BigCommerce receives this webhook, BigCommerce moves the payment status to captured. Note that BigCommerce will not update the order status. The orders status retains the status selected by the merchant. |
| `order.charge.capture.failed`   | BigCommerce surfaces a message to the merchant in the order timeline and order in the store log. No change to payment status or order status.                                                                    |
| `order.charge.cancelled`        | BigCommerce updates payment status to void, and order status to cancelled.                                                                                                                                       |
| `order.charge.refund.complete`  | Informational only. Indicates the refund on the order is complete.                                                                                                                                               |
| `order.charge.refund.failed`    | Informational only. Indicates the refund on the order failed. BigCommerce will set the payment and order status when the client performs the refund action on the UI or API                                      |
| `order.chargeback`              | BigCommerce will not change any payment status or order status. It will just display a message in the order tmeline.                                                                                             |
| `order.complete`                | Informational only. Indicates the order is complete.                                                                                                                                                             |



