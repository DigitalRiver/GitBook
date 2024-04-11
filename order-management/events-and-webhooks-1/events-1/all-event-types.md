---
description: Learn about all event types based on service or feature.
---

# All event types

Read this topic to learn about all available event types. The following sections provide the names and descriptions of available event types based on service or feature.

* [Account management events](all-event-types.md#account-management-events)
* [Checkout-related events](all-event-types.md#checkout-related-events)
* [Customer management events](all-event-types.md#customer-management-events)
* [Fee management events](all-event-types.md#fee-management-events)
* [File link events](all-event-types.md#file-link-management-events)
* [Fulfiller management events](all-event-types.md#fulfiller-management-events)
* [Fulfillment management events](all-event-types.md#fulfillement-management-events)
* [Global returns events](all-event-types.md#global-returns-events)
* [Invoice events](all-event-types.md#invoice-events)
* [Invoice attribute events](all-event-types.md#invoice-attribute-events)
* [Location management events](all-event-types.md#location-management-events)
* [Logistics events](all-event-types.md#logistics-events)
* [Manufacturer management events](all-event-types.md#manufacturer-management-events)
* [Order events](all-event-types.md#order-events)
* [Payout events](all-event-types.md#payout-events)
* [Plan events](all-event-types.md#plan-events)
* [Refund events](all-event-types.md#refund-events)
* [Return events](all-event-types.md#return-events)
* [Sales transaction events](all-event-types.md#sales-transaction-events)
* [SKU management events](all-event-types.md#sku-management-events)
* [Source events](all-event-types.md#source-events)
* [Subscription events](all-event-types.md#subscription-events)
* [Tax identifier management events](all-event-types.md#tax-identifier-management-events)

## Account management events

If you're using Digital River's account management service, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `account.update.failure:` Occurs whenever an account update fails.
* `account.update.success:` Occurs whenever an account update succeeds.

## Checkout-related events

If you're using Digital River's checkout service, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `checkout.created`: Occurs whenever a checkout is created.&#x20;
* `checkout.deleted:` Occurs whenever a checkout is deleted.&#x20;
* `checkout.updated:` Occurs whenever a checkout is updated.&#x20;
* `checkout_session.order.create:` Occurs from the orchestration service when an order is successfully created using a checkout session. The orchestration service will provide the full payload required to publish the event externally. This event requires no additional API requests to be made.

## Customer management events

If you're using Digital River's customer management service, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `customer.created`: Occurs whenever a customer is created.
* `customer.deleted`: Occurs whenever a customer is deleted.&#x20;
* `customer.invoice_attribute.created`: Occurs when an invoice attribute is attached to a customer.
* `customer.source.created:`Occurs whenever a source is attached to a customer.&#x20;
* `customer.source.deleted:`Occurs whenever a source is detached from a customer.&#x20;
* `customer.tax_identifier.created:`Occurs whenever a tax identifier is attached to a customer.&#x20;
* `customer.updated:`Occurs whenever a customer is updated.

## Fee management events

If you're using fees in your transactions, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `fee.created`: Occurs whenever a fee is created.
* `fee.deleted`: Occurs whenever a fee is deleted.&#x20;
* `fee.updated`: Occurs whenever a fee is updated.

## File link management events

If you're using file links in your transactions (for example, Prebuilt checkouts), you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `fileLink.created`: Occurs whenever a file link is created.
* `fileLink.deleted`: Occurs whenever a file link is deleted.
* `fileLink.updated`: Occurs whenever a file link is updated.

## Fulfiller management events

If you're managing order fulfillers, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `fulfiller.created`: Occurs when a fulfiller is created.&#x20;
* `fulfiller.deleted`: Occurs when a fulfiller is deleted.
* `fulfiller.updated`: Occurs when a fulfiller is updated.

## Fulfillment management events

If you're managing order fulfillments, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `fulfillment.create`: Occurs whenever an order item or an entire order is fulfilled by GF (Global Fulfillment) or a third party.&#x20;
* `fulfillment_cancellation.accepted`: Occurs when GF is notified that the fulfillment location has approved canceled products.
* `fulfillment_cancellation.created`: Occurs when a cancel request notification is sent to GF and has not yet been approved or rejected by the fulfillment location.&#x20;
* `fulfillment_cancellation.rejected`: Occurs when GF is notified that the fulfillment location has rejected canceled products.
* `fulfillment_order.backordered`: Occurs when GF receives a fulfillment status notice (status: back-ordered) from a channel's fulfiller.
* `fulfillment_order.cancelled`: Occurs when cancellation is auto-approved or cancellation request is approved through GFCC or fulfillment cancellation response.
* `fulfillment_order.pending`: Occurs when a sales order is enqueued for creation at GF
* `fulfillment_order.shipped`: Occurs when GF receives a shipment notification from a channel's fulfiller.
* `fulfillment_return.accepted`: Occurs when GF is notified that the fulfillment location has received returned products.
* `fulfillment_return.created`: Occurs when a return request notification is sent to GF and has not yet been approved or rejected by the fulfillment location.
* `fulfillment_return.pending`: Occurs when GF is notified that the fulfillment location has approved a return but is waiting in a pending state to be received at the warehouse.
* `fulfillment_return.rejected`: Occurs when GF is notified that the fulfillment location has rejected the return.

## Global returns events

If you're monitoring global returns status, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `global_returns.accepted`: Occurs when international returns are accepted.
* `global_returns.canceled`: Occurs when global returns are canceled.
* `global_returns.created`: Occurs when global returns are created.
* `global_returns.label.created`: Occurs when global return Labels are created.
* `global_returns.scanned:` Occurs when global returns are scanned.

## Invoice events

If you're monitoring invoice status, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `invoice.created:` Occurs whenever an invoice is created.
* `invoice.open:` Occurs whenever an invoice is opened.&#x20;
* `invoice.paid:` Occurs whenever an invoice is paid.&#x20;
* `invoice.payment_failed`: Occurs when an invoice is failed to capture the payment
* `invoice.uncollectible`: Occurs whenever an invoice state becomes uncollectible at the end of the payment collection period.&#x20;
* `invoice.updated:` Occurs whenever an invoice is updated.
* `invoice.void:` Occurs whenever an invoice is void.

## Invoice attribute events

If you're monitoring invoice attributes, you'll most likely want to [configure a webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `invoice_attribute.created:` Occurs when an invoice attribute is created.
* `invoice_attribute.deleted:` Occurs when an invoice attribute is deleted.

## Location management events

If you're managing locations, you'll most likely want to [configure a webhook(s)](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `location.created`:  Occurs when a location is created.
* `location.deleted`: Occurs when a location is deleted.
* `location.updated`: Occurs when a location is updated.

## Logistics events

If you're monitoring logistic returns status, you'll most likely want to [configure a webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [type(s](./#event-types)) of [event(s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)):

* `logistics_return.received`: Occurs when Global Logistics (GL) receives notification from a logistics partner that a return shipment has been received and accepted.

## Manufacturer management events

If you're managing manufacturer information, you'll most likely want to [configure a webhoo](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md)k to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `manufacturer.created:` Occurs whenever a manufacturer is created.
* `manufacturer.deleted`: Occurs whenever a manufacturer is deleted.
* `manufacturer.updated:`Occurs whenever a manufacturer is updated.

## Order events

If you're monitoring order status, payments, charges, refunds, and more, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* [`order.accepted`](event-types.md#order.accepted): Occurs whenever an order is submitted.&#x20;
* `order.blocked:` Occurs whenever an order is blocked (e.g., the customer is a denied person) or is blocked by fraud.
* `order.cancelled`: Occurs whenever an order is canceled.&#x20;
* `order.charge.cancel.complete`: Occurs whenever an order charge cancel is completed.
* `order.charge.cancel.failed`: Occurs whenever an order charge cancellation has failed.
* `order.charge.cancel.pending`: Occurs whenever an order charge cancellation is initiated.
* `order.charge.cancel.pending_information`: Occurs whenever an order charge cancel is initiated and awaiting information.
* `order.charge.cancelled`: Occurs whenever an order has all its charges canceled.
* `order.charge.capturable`: Occurs whenever an order charge becomes capturable
* `order.charge.capture.complete`: Occurs whenever an order charge capture is completed.
* `order.charge.capture.completed:` Occurs whenever an order charge capture completes. Replaced succeeded with completed.
* `order.charge.capture.created`: Occurs whenever a charge capture for all or part of an order charge is created.
* `order.charge.capture.failed`: Occurs whenever a payment (charge capture for all or part of an order) charge fails.
* `order.charge.capture.pending`: Occurs whenever an order charge capture is made.
* `order.charge.complete`: Occurs whenever an order charge is complete
* `order.charge.completed`: Occurs whenever an order charge is complete
* `order.charge.created`: Occurs whenever an order charge is created.
* `order.charge.failed`: Occurs whenever an order charge fails.
* `order.charge.pending`: Occurs whenever an order charge is created.
* `order.charge.reauth.failed`: Occurs when the reAuth fails during fulfillment
* `order.charge.refund.complete`: Occurs whenever an order charge refund is completed.
* `order.charge.refund.completed`: Occurs whenever an order charge refund completes
* `order.charge.refund.created`: Occurs whenever an order charge refund is created
* `order.charge.refund.failed`: Occurs whenever an order charge refund fails
* `order.charge.refund.pending`: Occurs whenever an order charge refund is created
* `order.chargeback`: Occurs whenever a chargeback Sales Transaction is created.
* `order.complete`: Occurs whenever an order is both fulfilled and captured.
* `order.created`: Occurs whenever an order is created.
* `order.credit_memo.create`d: Occurs whenever an order credit memo is created
* `order.dispute`: Occurs whenever an order gets disputed.
* `order.dispute.resolved`: Occurs whenever an order Dispute gets resolved.
* `order.fulfilled`: Occurs whenever all items in an order have been fulfilled (by GF, a third party, or both).
* `order.invoice.created`: Occurs when an order invoice is created.
* `order.pending_payment:` Occurs whenever an order is pending funds.
* `order.refunded:` Occurs whenever an order is refunded in part or in full.
* `order.review_closed`: Occurs whenever an order passes fraud or DPL review.
* `order.review_opened`: Occurs whenever an order enters fraud or DPL review
* `order.submitted`: Occurs whenever an order is submitted.
* `order.updated`: Occurs whenever an order is updated except for SKU item metadata, which won't generate order update events.

## Payout events

If you're monitoring payout status, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* `payout.created`: Occurs whenever a payout gets created.

## Plan events

If you're monitoring plan status, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `plan.created`: Occurs whenever a plan is created.&#x20;
* `plan.deleted`: Occurs whenever a plan is deleted.&#x20;
* `plan.updated`: Occurs whenever a plan is updated.

## Refund events

If you're monitoring the status of refunds, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `refund.complete`: Occurs whenever a refund occurs for all or part of an order.
* `refund.created`: Occurs whenever a refund is created for all or part of an order
* `refund.failed`: Occurs whenever an order refund fails.&#x20;
* `refund.pending`: Occurs whenever a refund is made.&#x20;
* `refund.pending_information`: Occurs whenever a refund needs additional information for processing.&#x20;
* `refund.succeeded`: Occurs whenever a refund occurs for all or part of an order.
* `refund.updated`: Occurs whenever the metadata for a refund is updated.

## Return events

If you're monitoring the status of returns, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `return.accepted`: Occurs whenever a return is accepted (all items defined in the return).
* `return.created`: Occurs whenever a return is created, including partial returns.
* `return.updated`: Occurs whenever the metadata for a return is updated.

## Sales transaction events

If you're monitoring sales transactions, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `sales_transaction.created`: Occurs whenever a sales transaction gets created.&#x20;

## SKU management events

If you're monitoring SKUs, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `sku.created:` Occurs whenever a SKU is created.&#x20;
* `sku.deleted`: Occurs whenever a SKU is deleted.&#x20;
* `sku.updated`: Occurs whenever a SKU is updated.

## Source events

If you're monitoring source status, you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `source.chargeable`: Occurs whenever a source transitions to chargeable.&#x20;
* `source.created`: Occurs whenever a source is created.

## Subscription events

If you're monitoring the status of [subscriptions](../../../subscription-management/managing-a-subscription.md), you'll most likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)[:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `subscription.created:` Occurs whenever a subscription is created.&#x20;
* `subscription.deleted`: Occurs whenever a subscription is deleted.&#x20;
* `subscription.extended`: Occurs whenever the subscription is renewed successfully.
* `subscription.failed`: Occurs whenever a subscription is failed.
* [`subscription.lapsed`](../../../subscription-management/managing-a-subscription.md#invalid-sources-and-lapsed-subscriptions): Occurs when the subscription grace date is past or equal to the lapse event date.
* `subscription.payment_failed`: Occurs when we send payment failure to the customer.
* `subscription.reminder`: Occurs when we send the customer a renewal reminder.
* [`subscription.source_invalid`](../../../subscription-management/managing-a-subscription.md#invalid-sources-and-lapsed-subscriptions): Occurs when a `source_not_supported` error occurs on renewal of subscription.
* `subscription.updated`: Occurs whenever a subscription is updated.

## Tax identifier management events

If you're managing tax identifier status and information, you'll likely want to [configure webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the following [types](./#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)[:](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)

* `tax_identifier.deleted`: Occurs whenever a tax identifier is deleted.
* `tax_identifier.not_valid`: Occurs whenever the state of tax identifier is changed to `not_valid`.
* `tax_identifier.pending`: Occurs whenever the state of tax identifier is changed to `pending`.
* `tax_identifier.updated`: Occurs whenever the content of a tax-identifier is updated (except state).
* `tax_identifier.verified`: Occurs whenever the state of a tax-identifier is changed to `verified`.
