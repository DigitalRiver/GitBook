---
description: Learn more about the standards related to building customer portals.
---

# Customer portal

The checklist items and standards in this section cover the building of a customer portal in the storefront's user interface. This customer portal should allow customers to store default shipping addresses, save payment methods for future use, review orders, and access links to their invoices and credit memos.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [Using the Events, Files, and FileLinks APIs, do you provide a method for Digital River generated invoices to be emailed to customers or retrieved through your storefront UI?](customer-portal.md#provide-a-method-for-customers-to-access-invoices-and-credit-memos)
* [ ] [Outside of a typical checkout flow, does your integration allow customers to use their account portal to save a payment method for future use?](customer-portal.md#allow-customers-to-use-their-account-portal-to-save-payment-methods)

## Integration standards

These integration standards relate to building customer account portals:

### Provide order invoice and credit memo notifications and download access

Your integration must allow customers to [access an order's invoice and any credit memo files](../../../order-management/creating-and-updating-an-order.md#tax-invoices-and-credit-memos). Once Digital River generates these files, we notify you by sending either the `order.invoice.created` or `order.credit_memo.created` event. You can use these events to create publicly accessible [links](../../../developer-resources/digital-river-api-reference/file-links/) to the documents and then send the links to the customer through email, text message, or another method of your choice.

Beyond these notifications, you must also provide customers access to the file links so they can download them through their account or order detail pages.

### Allow customers to use their account portal to save payment methods

Your integration's payment workflows should [allow customers to use their account portal to save a payment method](../../../integration-options/checkouts/building-you-workflows/#saving-a-credit-card-for-future-use). When setting up this account management flow, the key step is to configure [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) to [manage payment methods](../../../integration-options/checkouts/building-you-workflows/#account-management-flows). If configured correctly, Drop-in renders the payment method entry form. Once the customer supplies payment information and Digital River returns a [chargeable payment source](../../../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created), you can use its identifier to [attach the source to the customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

## API interfaces

| Documentation                                                                                                                                            | Direct API                                                                                 | PHP SDK                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| [Files](../../../developer-resources/digital-river-api-reference/files.md)                                                                               | [Files](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files)          | [Files](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/File.md)          |
| [File-links](../../../developer-resources/digital-river-api-reference/file-links/)                                                                       | [File-links](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/FileLinks) | [File-links](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/FileLink.md) |
| [Orders](../../../developer-resources/digital-river-api-reference/orders/)                                                                               | [Orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)        | [Orders](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Order.md)        |
| [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started) |                                                                                            |                                                                                                  |
| [Drop-in payments](../../../payments/payment-integrations-1/drop-in/)                                                                                    |                                                                                            |                                                                                                  |
| [Customers](../../../customer-management/customers.md)                                                                                                   | [Customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers)  | [Customers](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Customer.md)  |
| [Events](../../../order-management/events-and-webhooks-1/events-1/): file.created, file-link.created                                                     | [Events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)        |                                                                                                  |
