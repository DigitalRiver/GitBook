---
description: Learn more about the standards related to synchronizing order refund data.
---

# Order refund synchronization

The [checklist items](order-refund-synchronization.md#integration-checklist) and [standards](order-refund-synchronization.md#integration-standards) in this section cover how to consume refund and chargeback events and use them to update order refund data in your commerce system. This helps ensure that throughout the entire order life cycle, the data in your system stays in sync with the data in Digital River's system.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [After consuming an `order.charge.refund.complete` event, do you update the order refund status and other refund data in your commerce system?](order-refund-synchronization.md#consume-refund-complete-event-and-update-refund-data)
* [ ] [After consuming an `order.chargeback` event, do you update the order refund status and other refund data in your commerce system?](order-refund-synchronization.md#consume-chargeback-event-and-update-refund-data)

## Integration standards

These integration standards relate to synchronizing order refund states:

### Consume refund complete event and update refund data

After you [provide notification of a refund](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md), Digital River processes your request and emits refund-related [events](../../../order-management/events-and-webhooks-1/events-1/) to your [webhooks](../../../order-management/events-and-webhooks-1/webhooks/). When you receive the `refund.complete` and `order.charge.refund.complete` events, update your commerce system with the `state` value, and other information, delivered in the events.

### Consume chargeback event and update refund data

When Digital River processes and completes a chargeback, we create a [Sales Transaction](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/developer-resources/standards-and-certifications/integration-checklists/broken-reference/README.md) with a `type` of `fraud_chargeback` or `non_fraud_chargeback` and send you both a `sales_transaction.created` and `order.chargeback` event. You should use the `order.chargeback` event to update the status of the order refund in your commerce system.

## API interfaces

| Documentation                                                                                                       | Direct API                                                                          | PHP SDK                                                                                   |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [Events](../../../order-management/events-and-webhooks-1/events-1/): order.charge.refund.complete, order.chargeback | [Events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) | [Events](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Event.md) |
