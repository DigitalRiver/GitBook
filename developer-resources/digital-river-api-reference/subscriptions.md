---
description: Learn more about the subscriptions resource
---

# Subscriptions

On this page, you'll find information on:

* [The subscriptions resource](subscriptions.md#the-subscriptions-resource)
* [The lifecycle of a subscription](subscriptions.md#lifecycle-of-a-subscription)

## The subscriptions resource

The following describes some of the key attributes in a [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions).&#x20;

### Binding period

The `contractBindingUntil` attribute represents the date and time when the subscription's contract expires. It's determined by adding the [plan's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) [`contractBindingDays`](plans.md#contract-length-and-interval) to the [subscription's activation date](../../subscription-management/managing-a-subscription.md#activating-a-subscription).

The data in this field doesn't drive any logic. Instead, it exists for compliance and transparency purposes. All subscriptions are open-ended. This means that they keep billing until the subscription's [`state`](subscriptions.md#state) is `cancelled`, `ended`, `lapsed`, or `failed`.

It's assumed, however, that your integration will allow customers to [cancel a subscription](../../subscription-management/managing-a-subscription.md#cancelling-a-subscription) once the `contractBindingUntil` date elapses. Failing to honor a customer's valid cancellation request makes you vulnerable to [chargebacks](../../order-management/returns-and-refunds-1/disputes-and-chargebacks.md).

When a customer wants to cancel a subscription prior to the `contractBindingUntil` date, it's up to the client-system to decide whether to honor the request.

### State

For details, refer to the [lifecycle of a subscription](subscriptions.md#lifecycle-of-a-subscription) section.

### Plan identifier

The `planId` uniquely identifies the [plan](plans.md) that the subscription belongs to.

### Billing agreement identifier

For more information on the `billingAgreementId`, refer to the [billing agreements](../../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreements) section on the [Subscription information](../../integration-options/checkouts/subscriptions/subscription-information-1.md) page.

### Customer and source identifiers

The [`customerId`](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and [`sourceId`](../../payments/payment-sources/using-the-source-identifier.md) are inherited from the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

### Tax inclusivity

The [`taxInclusive`](../../integration-options/checkouts/creating-checkouts/configuring-taxes.md) value is inherited from the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

### Subscription products and services

The price, quantity, and SKU identifier of the subscription's products and services are contained in `items[]`.&#x20;

### Current period start date

The `currentPeriodStartDate` represents the date and time when the subscription's current billing period began. This value, added to the [plan's `interval`](plans.md#contract-length-and-interval), equals the subscription's [`currentPeriodEndDate`](subscriptions.md#current-period-end-date).

### Current period end date

The `currentPeriodEndDate` represents the date and time when the subscription's current billing period ends. Subtracting the [plan's `interval`](plans.md#contract-length-and-interval) from this value gives you the subscription's [`currentPeriodStartDate`](subscriptions.md#current-period-start-date).

### Date of next invoice

The `nextInvoiceDate` represents the date and time of the next billing attempt. It's when Digital River [opens a new invoice](invoices.md#invoice-states) and starts attempting to capture payment. The value is determined by subtracting the [plan's `billingOffsetDays`](plans.md#billing-offset) from the subscription's [`currentPeriodEndDate`](subscriptions.md#current-period-end-date).

For example, a subscription with a `currentPeriodEndDate` of `2021-08-06T00:00:00.0000000Z` that belongs to a plan with a `billingOffsetDays` of `5`, will have a `nextInvoiceDate` of `2021-08-01T00:00:00.0000000Z`.

### Date of next reminder

The `nextReminderDate` is the date and time when Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`subscription.reminder`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.reminder).

## Lifecycle of a subscription

Once the acquisition [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) is created, Digital River determines whether the [plan](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) is [`active`](plans.md#state), and, if it is, creates a [subscription](subscriptions.md) whose `state` is `draft`.

After you [activate the subscription](../../subscription-management/managing-a-subscription.md#activating-a-subscription), we determine whether (1) the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) exists, (2) its [`state`](orders/the-order-lifecycle.md#order-states-and-events) is `accepted` and (3) the subscription's [payment source](../../payments/payment-sources/) remains valid. If these conditions are met, we move the subscription's `state` to either `active` or `activeFree`.

{% hint style="info" %}
For details about `activeFree`, refer to [Using free trials](../../using-our-services/subscriptions.md#setting-up-free-trials).
{% endhint %}

On the subscription's [`nextReminderDate`](subscriptions.md#date-of-next-reminder), Digital River retrieves data from the resource and uses it to create a [`draft`](invoices.md#invoice-states) [invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices). We then add `subscription` and [`invoice`](invoices.md) to the [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`subscription.reminder`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.reminder).

On the subscription's [`nextInvoiceDate`](subscriptions.md#date-of-next-invoice), Digital River checks the [invoice's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) `totalAmount`. If its `0`, then this indicates that the subscription's free trial period has either been extended or reactivated and, as a result, we don't make any payment collection attempts and the subscription's `state` either remains or becomes `activeFree`.

If the invoice's `totalAmount` is greater than `0`, then we move its [`state`](invoices.md#invoice-states) to `open`, which initiates the billing process and pushes the subscription's `state` to `activePendingInvoice`.

If we immediately capture payment, then the invoice becomes [`paid`](invoices.md#invoice-states), the subscription transitions to `active` and [`subscription.extended`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.extended) is triggered.

If we're unable to synchronously capture payment, then the subscription's `state` remains `activePendingInvoice`. This indicates that our [smart auto-renewal service](invoices.md#invoice-billing) is still attempting to collect payment.

The service continues making billing attempts until either (1) payment is successfully captured or (2) the [collection period](plans.md#collection-period-days) elapses. A successful billing attempt moves the subscription's `state` to `active` and triggers the creation of [`subscription.extended`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.extended). If the invoice is ultimately [`uncollectible`](invoices.md#invoice-states), then the subscription's `state` becomes `failed`, which is a terminal condition, and [`subscription.failed`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.failed) is created.

Three other terminal states might occur during a subscription's lifecycle: `ended`, `lapsed`, and `cancelled`.

If you [discontinue a subscription's plan](../../using-our-services/subscriptions.md#discontinuing-and-deactivating-plans), then `state` remains `active` and the subscription continues billing. But if you [deactivate a subscription's plan](../../using-our-services/subscriptions.md#discontinuing-and-deactivating-plans), then `state` becomes `ended` on its [`nextInvoiceDate`](subscriptions.md#date-of-next-invoice), at which point recurring billing permanently stops.

If we can’t create a [billing invoice](invoices.md) because it's determined that the subscription's designated [source](../../payments/payment-sources/) has a problem, then [`subscription.source_invalid`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.source\_invalid) is triggered but the subscription's `state` remains `active`. However, if the invalid source isn’t replaced at some point during the grace period (i.e., the [`collectionPeriodDays`](plans.md#collection-period-days) of the subscription’s plan), then `state` moves to `lapsed`.

The remaining terminal `state` is `cancelled`, which means that a [cancel subscription request](../../subscription-management/managing-a-subscription.md#cancelling-a-subscription) has been successfully submitted.



<figure><img src="../../.gitbook/assets/Subscription lifecycle (2).png" alt=""><figcaption></figcaption></figure>

The following table looks at what precedes a subscription `state` change and which types of events (if any) are created as a result:

<table data-header-hidden><thead><tr><th width="308"></th><th width="218.33333333333331"></th><th></th></tr></thead><tbody><tr><td>(1) When...</td><td>(2) the subscription's <code>state</code>...</td><td>(3) and an event with a <code>type</code> of ... is created.</td></tr><tr><td>the acquisition <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts">checkout</a>  is created</td><td>becomes <code>draft</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.created"><code>subscription.created</code></a></td></tr><tr><td>the subscription is activated</td><td>switches to <code>active</code> or <code>activeFree</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.updated"><code>subscription.updated</code></a></td></tr><tr><td>Digital River synchronously or asynchronously captures a recurring payment</td><td>becomes <code>active</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.extended"><code>subscription.extended</code></a></td></tr><tr><td>Digital River <em>cannot</em> immediately capture a recurring payment</td><td>switches to <code>activePendingInvoice</code></td><td>--</td></tr><tr><td>Digital River fails to capture a recurring payment</td><td>switches to <code>failed</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.failed"><code>subscription.failed</code></a></td></tr><tr><td>Digital River determines that the subscription's <a href="../../payments/payment-sources/">source</a> is invalid</td><td>remains <code>active</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.source_invalid"><code>subscription.source_invalid</code></a></td></tr><tr><td>An invalid <a href="../../payments/payment-sources/">source</a> is not replaced during the grace period</td><td>moves to <code>lapsed</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.lapsed"><code>subscription.lapsed</code></a></td></tr><tr><td>the subscription  cancelled</td><td>moves to <code>cancelled</code></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.updated"><code>subscription.updated</code></a></td></tr><tr><td>the subscription's <a href="subscriptions.md#the-plans-object">plan</a> is deactivated</td><td>switches to <code>ended</code> on <a href="subscriptions.md#date-of-next-invoice"><code>nextInvoiceDate</code></a></td><td>--</td></tr><tr><td>the subscription is deleted</td><td><em>(subscription no longer exists)</em></td><td><a href="../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.deleted"><code>subscription.deleted</code></a></td></tr></tbody></table>
