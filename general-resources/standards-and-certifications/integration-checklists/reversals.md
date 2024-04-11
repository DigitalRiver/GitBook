---
description: Learn more about the standards related to performing reverse logistics.
---

# Reversals

The [checklist items](reversals.md#integration-checklist) and [standards](reversals.md#integration-standards) in this section cover how to perform reverse logistics related to refunds and returns.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [Using the Refunds API, can you initiate a refund request from the admin portal of your commerce system?](reversals.md#initiate-refunds-in-your-admin-portal)
* [ ] [Using the Refunds API, can you display details about previous refund requests from the admin portal of your commerce system](reversals.md#display-refund-information-in-your-admin-portal)?

## Integration standards

These integration standards relate to reversals:

### Initiate refunds in your admin portal

In your commerce system's admin portal, you should build a mechanism for [submitting refund requests](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md#refund-requests). When you build this feature, you should also ensure that you can capture and display any [failure reasons](../../../order-management/returns-and-refunds-1/refunds/#dealing-with-refund-failures) returned by a call to the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds).

### Display refund information in your admin portal

In your commerce system's admin portal, you should build a mechanism that [searches for previously requested refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listRefunds) and displays that information. This information should be available on a per-order basis using the [Orders resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and per-refund using the [Refunds resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds).

## API interfaces

| Documentation                                                                                                       | Direct API                                                                            | PHP SDK                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| [Refunds](../../../order-management/returns-and-refunds-1/refunds/)                                                 | [Refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) | [Refunds](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Refund.md)              |
| [Returns](../../../order-management/returns-and-refunds-1/returns/)                                                 | [Returns](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) | [ReturnRequest](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/ReturnRequest.md) |
| [Events](../../../order-management/events-and-webhooks-1/events-1/): refund.created, refund.failed, refund.complete | [Events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)   |                                                                                                          |
