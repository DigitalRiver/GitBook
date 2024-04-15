---
description: Learn more about the invoices resource
---

# Invoices

{% hint style="warning" %}
The [invoice resource](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) is only available in versions `2020-09-30` and higher.
{% endhint %}

In the Digital River APIs, an [invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) represents a document, associated with a sale, that you provide to customers. Invoices itemize products or services rendered and include their cost, quantity, fees, duties, and taxes. They also establish an obligation on the part of customers to pay you for the goods.

Invoices are especially useful when selling to other businesses. In business-to-business transactions, it's often customary to send customers an invoice, which they pay at a later time, rather than immediately billing a credit card on file.

You use the [Invoices API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) to [manage invoices](invoices.md#managing-invoices) . This API allows you to [create invoices](invoices.md#creating-an-invoice) for one-off transactions or to set up subscriptions and start billing them.

If you integrate with the [Invoices API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices), we recommend you familiarize yourself with the [invoice lifecycle](invoices.md#invoice-states) as well as the [invoice billing process](invoices.md#invoice-billing).

## Managing invoices

You can [create](invoices.md#creating-an-invoice), [open](invoices.md#opening-an-invoice), [void](invoices.md#voiding-an-invoice), and [delete](invoices.md#deleting-an-invoice) invoices. The process of [collecting payment](invoices.md#invoice-billing) on invoices is entirely handled by Digital River. After an invoice is paid, you can use the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) to [issue refunds](invoices.md#refunding-an-invoice) any needed refunds.

### Creating an invoice

In a [`POST/invoices`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createInvoices) request, you can set [`state`](invoices.md#invoice-states) to either `draft` or `open`. The default value is `open`.

If you'd like us to immediately start the [billing process](invoices.md#invoice-billing), set `state` to `open`.

Creating a `draft` invoice means you haven't yet authorized Digital River to capture any charges. However, draft invoices do list the total taxes, fees, duties, and amounts for the goods rendered. As a result, they can be useful to include in billing reminders to customers.

Invoices are created in much the same way as [checkouts](../creating-checkouts/). The major difference is that invoices allow you to [optimize billing](invoices.md#invoice-billing). Additionally, invoices can only be used to sell [digital products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), so you can't send any ship from values.

The following provides more information on the key parameters you can set when creating an invoice. For complete specifications, refer to the [Invoices API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) reference page.

| Parameter              | Documentation                                                                                                                                                                      |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customerId`           | [Registered invoices](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices)                                                                     |
| `sourceId`             | [Supported payment methods](../../../payments/payment-sources/#supported-payment-methods) and [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md) |
| `currency`             | [Selecting a currency](../creating-checkouts/selecting-a-currency.md)                                                                                                              |
| `state`                | [The invoice lifecycle](invoices.md#the-invoice-lifecycle)                                                                                                                         |
| `locale`               | [Designating a locale](../creating-checkouts/designating-a-locale.md)                                                                                                              |
| `shipTo`               | [Ship to address](../creating-checkouts/providing-address-information.md#ship-to-address)                                                                                          |
| `discount`             | [Checkout level discount](../creating-checkouts/applying-a-discount.md#checkout-level-or-invoice-level-discount)                                                                   |
| `collectionPeriodDays` | [Invoice billing](invoices.md#invoice-billing)                                                                                                                                     |
| `billingOptimization`  | [Invoice billing](invoices.md#invoice-billing)                                                                                                                                     |
| `items`                | [Describing the items](../creating-checkouts/describing-the-items/)                                                                                                                |
| `taxInclusive`         | [Configuring taxes](../creating-checkouts/configuring-taxes.md)                                                                                                                    |
| `taxIdentifiers`       | [Tax identifiers](../creating-checkouts/tax-identifiers.md)                                                                                                                        |
| `chargeType`           | [Initiating a charge](../creating-checkouts/initiating-a-charge.md)                                                                                                                |
| `customerType`         | [Using customer type](../creating-checkouts/setting-the-customer-type.md)                                                                                                          |
| `upstreamId`           | [Providing an upstream identifier](broken-reference)                                                                                                                               |

### Opening an invoice

To open an already created invoice, send a [`POST/invoices/{id}/open`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/openInvoices). Only `draft` invoices can be opened. So, before sending the request, make you first determine the invoice's `state`.

By opening an invoice, you're instructing Digital River to initiate the [billing process](invoices.md#invoice-billing).

Once opened, none of an invoice's attributes, other than `metadata`, can be updated. If you need to update customer or amount attributes, then [void the invoice](invoices.md#voiding-an-invoice) and create a new one.

### Voiding an invoice

To void an invoice, send a [`POST/invoices/{id}/void`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/voidInvoices) request . This operation is similar to [deleting an invoice](invoices.md#deleting-an-invoice) but it allows you to maintain a record of when the invoice was [created](invoices.md#creating-an-invoice), [opened](invoices.md#opening-an-invoice), and voided.

Invoices in a voided state are not payable. If you receive payment from the customer outside of the normal flow (e.g., the customer pays by check) you should void the invoice. This is also a terminal state, which means voided invoices can't transition to another state.

Only `open` invoices can be voided. If an invoice is in any other state, and you attempt to void it, a `409 Conflict` is thrown:

{% tabs %}
{% tab title="Error" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_state",
            "parameter": "state",
            "message": "Invoice 4fce39e4549845cf9d571a7676842a90 is not open. Only open invoices can be voided."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Deleting an invoice

To permanently delete an invoice, send a [`DELETE/invoices/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteInvoices) request . This operation is similar to [voiding an invoice](invoices.md#voiding-an-invoice) but no record is maintained for accounting purposes. Only `draft` invoices can be deleted.

### Refunding an invoice

Use the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) to refund [charges](../../../order-management/orders/payment-charges/) that are [captured](../../../order-management/orders/payment-charges/#captures) when an invoice is paid. To partially or fully refund the invoice, send its `invoiceId` in a `POST/refunds`.

## Invoice billing

Once you move an [invoice's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) `state` to `open`, Digital River initiates a billing process and attempts to [capture the charge(s](../../../order-management/orders/payment-charges/#captures)). With invoices, you can take advantage of our [billing optimization feature](invoices.md#billing-optimization). If you use this feature, make sure your integration only displays [payment methods that are supported with invoices](invoices.md#supported-payment-methods).

### Billing optimization

The [Invoices API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) contains billing features that are not available in the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). To use them, set `billingOptimization` to `true`. This setting prompts Digital River to make multiple [payment capture attempts](../../../order-management/orders/payment-charges/#captures) throughout the billing period, the length of which you can configure by setting `collectionPeriodDays` (the default setting is 30).

If Digital River successfully capture the charge(s), we move the invoice's `state` to `paid`. If the charge(s) are still not captured at the end of `collectionPeriodDays`, we move the invoice's `state` to `uncollectible` and create an `invoice.uncollectible` event.

The number of times Digital River has attempted to collect payment is represented by the invoice's `attemptCount`. This value can be useful for your analytics.

If you set `billingOptimization` to `false`, Digital River makes just one payment collection attempt. In this case, `collectionPeriodDays` has no effect on the billing process. Depending on the result of that single collection attempt, we move the invoice's `state` to either `paid` or `uncollectible` and then [emit the corresponding event](invoices.md#invoice-events).

An expired credit card, insufficient funds, or a closed credit card account are all common reasons for an uncollectible invoice.

### Supported payment methods with invoices <a href="#supported-payment-methods" id="supported-payment-methods"></a>

If you set [`billingOptimization`](invoices.md#billing-optimization) to `false`, then you can allow customers to use any [supported payment method](../../../payments/supported-payment-methods/) to pay an [invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices). This includes [combining a primary source with one or more secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources).

If `billingOptimization` is `true`, then an [invoice's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) `payment.sources[]` should only contain a single [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources). Additionally, that object must be a [primary source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) and it must support [reusability](../../../payments/payment-sources/#reusable-or-single-use). So, if you're using the billing optimization feature, restrict customers to payment methods that can be used in recurring transactions.

For a complete list of such payment methods, refer to the [Supported payment methods ](../../../payments/supported-payment-methods/)page.

## The invoice lifecycle

An invoice has a defined lifecycle. Each time the [state of an invoice](invoices.md#invoice-states) changes, Digital River creates a corresponding [event](invoices.md#invoice-events).

### Invoice states

An invoice has the following states: `draft`, `open`, `paid`, `uncollectible`, or `void`.

Invoices in a `draft` state can either be [opened](invoices.md#opening-an-invoice), which both transitions them to an `open` state and initiates the [billing process](invoices.md#invoice-billing), or they can be [deleted](invoices.md#deleting-an-invoice) entirely.

An `open` invoice can then transition to `void`, `paid`, or `uncollectible`. All of these are terminal states. Invoices that are `void` or `uncollectible` are not payable.

![](<../../../.gitbook/assets/Invoice states (3).png>)

The `state` values for a successful invoice (i.e. the happy path) are `draft` > `open` > `paid` .

### Invoice events

When the [state of an invoice](invoices.md#invoice-states) changes, an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) that describes the change is created. For example, when an invoice's `state` changes from `open` to `paid` both an `invoice.paid` and an `invoice.updated` event are emitted.

All generated invoice events can be filtered and viewed by accessing the [Digital River Dashboard event log](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/event-logs).

| 1) When an invoice is...                                   | (2) its state transitions to... | (3) and Digital River creates an ... event       |
| ---------------------------------------------------------- | ------------------------------- | ------------------------------------------------ |
| created but not yet authorized for billing                 | `draft`                         | `invoice.created`                                |
| simultaneously created and authorized for billing          | `open`                          | `invoice.created` and an `invoice.open`          |
| already created as a draft and then authorized for billing | `open`                          | `invoice.open` and an `invoice.updated`          |
| authorized for billing and then paid                       | `paid`                          | `invoice.paid` and an `invoice.updated`          |
| authorized for billing and then voided                     | `void`                          | `invoice.void` and an `invoice.updated`          |
| authorized for billing but cannot be collected             | `uncollectible`                 | `invoice.uncollectible` and an `invoice.updated` |
