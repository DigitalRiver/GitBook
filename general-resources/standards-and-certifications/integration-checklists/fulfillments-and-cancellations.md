---
description: Learn more about the standards related to fulfilling or cancelling items.
---

# Fulfillments and cancellations

The [checklist items](fulfillments-and-cancellations.md#integration-checklist) and [standards](fulfillments-and-cancellations.md#integration-standards) in this section cover when and how to notify Digital River that you have [fulfilled or cancelled](../../../order-management/informing-digital-river-of-a-fulfillment.md) all or part of a transaction.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [After your system confirms a line item is fulfilled, do you use the Fulfillments API to supply Digital River with the required fulfillment data?](fulfillments-and-cancellations.md#provide-required-fulfillment-data)
* [ ] [After your system confirms a line item is cancelled, do you use the Fulfillments API to supply Digital River with the required cancellation data?](fulfillments-and-cancellations.md#provide-required-cancellation-data)

## Integration standards

These integration standards relate to fulfillments and cancellations:

### Provide required fulfillment data

Once you either [synchronously](../../../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an order in an `accepted` state, your integration can use the [Fulfillments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) to submit a [`POST/fulfillments`](../../../order-management/informing-digital-river-of-a-fulfillment.md) with a fulfilled quantity.

When all the items in an order are fulfilled, the [order transitions](../../../order-management/orders/the-order-lifecycle.md) to a `state` of `complete` and an `order.complete` event is emitted. After you receive this event, you should update the order status in your system to match its `state` in our system.

### Provide required cancellation data

To cancel items, your integration must use the [Fulfillments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) to submit a [`POST/fulfillments`](../../../order-management/informing-digital-river-of-a-fulfillment.md) with a cancel quantity.

## API interfaces

| Documentation                                                                            | Direct API                                                                                      | PHP SDK                                                                                               |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [Fulfillments](../../../order-management/fulfillments.md)                                | [Fulfillments](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) | [Fulfillments](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Fulfillment.md) |
| [Events](../../../order-management/events-and-webhooks-1/events-1/): fulfillment.created | [Events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)             |                                                                                                       |
