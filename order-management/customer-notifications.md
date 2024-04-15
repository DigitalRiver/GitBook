---
description: >-
  Gain a better understanding of what notifications to send to customers and
  what information to include in them
---

# Customer notifications

Throughout an e-commerce transaction, you'll need to send messages (typically emails) to your customers. The purpose of these notifications is to provide customers information on their purchase and inform them of important events. They also help keep your customers engaged throughout the entire process, leading to a more positive shopping experience and potentially increasing brand loyalty.

{% hint style="success" %}
To gain access to Digital River's [MOR/SOR](../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor) business model, you must send certain notifications to customers.                                                                                                                                                                                           &#x20;
{% endhint %}

In many cases, you can [configure webhook(s)](../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for [events](events-and-webhooks-1/events-1/) created by Digital River and then use the data in these events to populate the emails before they get pushed to customers.&#x20;

On this page, you'll find information on both [order notifications](customer-notifications.md#order-notifications) and [subscription notifications](customer-notifications.md#subscription-notifications) as well as the events in the Digital River APIs (when available) that can be used to trigger them.

## Order notifications

In this section, you'll find basic information on what notifications to send to customers throughout an [order's lifecycle](orders/the-order-lifecycle.md):

* [Order confirmation](customer-notifications.md#order-confirmation)
* [Shipment notification](customer-notifications.md#shipment-notification)
* [Successful cancellations](customer-notifications.md#successful-cancellation)
* [Failed cancellations](customer-notifications.md#failed-cancellation)
* [Delayed shipments, right to cancel](customer-notifications.md#delayed-shipment-right-to-cancel-1st-and-2nd-notices)
* [Refund confirmation](customer-notifications.md#refund-confirmation)
* [Product return instructions](customer-notifications.md#product-return-instructions)

### Order confirmation&#x20;

This notification informs your customers that their order has been approved and is currently being processed. It provides customers a record of their purchase and assures them that the transaction is authentic.

{% hint style="info" %}
In [Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=801ab0c1dbe99910df9cddf5f49619b5\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=7f6979591b516d500af5524f034bcbd9) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of triggering event**: [`order.accepted`](events-and-webhooks-1/events-1/event-types.md#order.accepted)

{% hint style="success" %}
This same event type can also be used for [subscription acquisition notifications ](customer-notifications.md#acquisition-confirmation).
{% endhint %}

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="281">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The identifier of the order</td><td><code>id</code></td></tr><tr><td>A description of each product</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url)</code> in <code>items[].productDetails</code></td></tr><tr><td>The cost of each product</td><td><code>items[].amount</code></td></tr><tr><td>Assessed taxes</td><td><code>totalTax</code></td></tr><tr><td>Applied discounts</td><td><code>totalDiscount</code></td></tr><tr><td>Shipping costs</td><td><code>totalShipping</code></td></tr><tr><td>Total amount of order</td><td><code>totalAmount</code></td></tr></tbody></table>

### Shipment notification

Send this notification to customers when some or all of an order's goods have shipped. The message must indicate which items are in the shipment and should ideally include delivery tracking information.&#x20;

{% hint style="info" %}
In [Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=801ab0c1dbe99910df9cddf5f49619b5\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=7f6979591b516d500af5524f034bcbd9) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of triggering event**: [`fulfillment.created`](events-and-webhooks-1/events-1/event-types.md#fulfillment.created)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="286">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The identifier of the order</td><td><code>orderId</code> or <code>orderDetails.id</code></td></tr><tr><td>A description of each shipped product</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url)</code> in <code>orderDetails.items[].productDetails</code></td></tr><tr><td>The quantity of each shipped product</td><td><code>items[].quantity</code></td></tr><tr><td>The name of the designated carrier</td><td><code>trackingCompany</code></td></tr><tr><td>The designated carrier's tracking number</td><td><code>trackingNumber</code></td></tr><tr><td>A url that allows customers to access tracking details</td><td><code>trackingUrl</code></td></tr></tbody></table>

### Successful cancellation

This notification informs customers that their order has been partially or fully cancelled.  Regardless of the reason for the cancellation or who initiated the request, purchasers need to be notified which items will not be fulfilled.&#x20;

{% hint style="info" %}
In [Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=801ab0c1dbe99910df9cddf5f49619b5\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=7f6979591b516d500af5524f034bcbd9) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of triggering event**: [`fulfillment.created`](events-and-webhooks-1/events-1/event-types.md#fulfillment.created) or [`order.cancelled`](events-and-webhooks-1/events-1/event-types.md#order.cancelled)

If your application supports partial order cancellations, then we recommend listening for `fulfillment.created` and using it to trigger this message.&#x20;

This is because the `state` of each `items[]` in an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) must be `cancelled` before Digital River creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-and-webhooks-1/events-1/#event-types) of `order.cancelled`.&#x20;

For example, if an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains multiple `items[]`, each with a `quantity` of `2`, and a customer uses your site’s UI to request that only one of those line items be fully cancelled, and, after approving that request, your system sends a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/createFulfillments) with an `items[].cancelQuantity` of `2`, then Digital River generates `fulfillment.created` but not `order.cancelled`.

Use the following tables to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

{% tabs %}
{% tab title="order.cancelled" %}
<table><thead><tr><th width="240">Notification information</th><th width="425">Relevant attribute </th></tr></thead><tbody><tr><td>The identifier of the order</td><td><code>id</code></td></tr><tr><td>A description of each cancelled product</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url)</code> in <code>items[].productDetails</code></td></tr><tr><td>The quantity of each cancelled product </td><td><code>items.quantity</code></td></tr></tbody></table>
{% endtab %}

{% tab title="fulfillment.created" %}
<table><thead><tr><th width="235">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The identifier of the order</td><td><code>orderId</code> or <code>orderDetails.id</code></td></tr><tr><td>A description of each cancelled product</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url)</code> in <code>orderDetails.items[].productDetails</code></td></tr><tr><td>The quantity of each cancelled product </td><td><code>items.cancelQuantity</code></td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Failed cancellation&#x20;

If customers request to have an order partially or fully cancelled, but, for whatever reason, you can't honor their request, send an notification informing them that their goods are still scheduled for fulfillment. &#x20;

{% hint style="info" %}
In [Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=801ab0c1dbe99910df9cddf5f49619b5\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=7f6979591b516d500af5524f034bcbd9) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

Unless [Digital River coordinates a fulfillment](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), there are no [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) in the Digital River APIs that can be used to trigger this failed cancellation message.&#x20;

### Delayed shipment, right to cancel (1st and 2nd notices)

If a shipment is delayed, send a notification to customers that provides a revised date of when the goods are scheduled for delivery. If additional delays occur that cause that date to be pushed out even further, send customers a second notice. In both of these messages, you must give customers the option to cancel their purchase.&#x20;

{% hint style="info" %}
In [Physical Goods Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=1267994ddba1d910df9cddf5f4961929\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=b2974e9d1b156d500af5524f034bcba7) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

In the Digital River APIs, there are currently no [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) that can be used to trigger these delayed shipment notifications. &#x20;

### Refund confirmation

This notification confirms that a customer's refund request has been successfully processed.&#x20;

{% hint style="info" %}
In [Required Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=801ab0c1dbe99910df9cddf5f49619b5\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=7f6979591b516d500af5524f034bcbd9) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this message.
{% endhint %}

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of triggering event**: [`order.refunded`](events-and-webhooks-1/events-1/event-types.md#order.refunded)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="234">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The order identifier</td><td><code>id</code></td></tr><tr><td>Total amount refunded on order</td><td><code>refundedAmount</code></td></tr><tr><td>The amount of each individual refund on the order (optional)</td><td><code>payment.charges[].refunds[].amount</code></td></tr></tbody></table>

### Product return instructions

This message provides instructions to customers on how to return [physical products](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) they've purchased.&#x20;

{% hint style="info" %}
In [Recommended Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=e6ef0909db21d910df9cddf5f4961920\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=9bf64a1d1b156d500af5524f034bcbb3) (refer to [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information), you'll find a comprehensive list of what to include in this notification.
{% endhint %}

Unless [Digital River coordinates a fulfillment](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/), no [events](events-and-webhooks-1/events-1/) currently exist in the Digital River APIs that can be used to trigger this message.

## Subscription notifications

In this section, you'll find basic information on what notifications to send customers throughout a subscription's lifecycle. We also provide guidance on each notification's potential [triggering event](customer-notifications.md#triggering-events).

{% hint style="info" %}
Refer to [Subscription Purchase Notifications](https://digitalriver.service-now.com/kb?sys\_kb\_id=e8c044671bc421540af5524f034bcb56\&id=kb\_article\_view\&sysparm\_rank=1\&sysparm\_tsqueryId=cf5635991b116d500af5524f034bcb56) (see [Learning tools](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information) to be provided with a comprehensive list of what's required and what's recommended in these messages.
{% endhint %}

* [Acquisition confirmation](customer-notifications.md#acquisition-confirmation)
* [Trial conversion notification](customer-notifications.md#trial-conversion-notification)
* [Renewal reminder](customer-notifications.md#renewal-reminder)
* [Renewal confirmation](customer-notifications.md#renewal-confirmation)
* [Subscription cancelled notification](customer-notifications.md#subscription-cancelled-notification)
* [Updated terms](customer-notifications.md#updated-terms)
* [Billing failed notification](customer-notifications.md#billing-failed-notification)
* [Subscription failed notification](customer-notifications.md#subscription-failed-notification)
* [Payment method expiration](customer-notifications.md#payment-method-expiration)

### Triggering events

If you're using [Digital River's subscription service](../using-our-services/subscriptions.md), we indicate which [`type`](events-and-webhooks-1/events-1/#event-types) of [event](events-and-webhooks-1/events-1/) can be used to trigger each [subscription notification](customer-notifications.md#subscription-notifications). However, if you engage a third-party subscription service, then (with the exception of [acquisition confirmation notifications](customer-notifications.md#acquisition-confirmation)), you'll need to listen for relevant triggering events emanating from that service.&#x20;

### Acquisition confirmation

This notification informs customers that they have successfully acquired one or more subscription-based products.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`order.accepted`](events-and-webhooks-1/events-1/event-types.md#order.accepted)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="269">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The identifier of the acquisition order</td><td><code>id</code></td></tr><tr><td>A description of each subscription product</td><td><p>For each <code>items[]</code> with <code>subscriptionInfo</code>, the</p><p><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url)</code> in <code>productDetails</code></p></td></tr><tr><td>The cost of each subscription product</td><td>For each <code>items[]</code> with <code>subscriptionInfo</code>, the <code>amount</code></td></tr><tr><td>Assessed taxes</td><td><code>totalTax</code></td></tr><tr><td>Applied discounts</td><td><code>totalDiscount</code></td></tr><tr><td>Shipping costs</td><td><code>totalShipping</code></td></tr><tr><td>Total amount of order</td><td><code>totalAmount</code></td></tr></tbody></table>

### Trial conversion notification

This notification informs customers that their promotional trial period has ended and in the future they will be billed on a recurring basis for the subscription's products. &#x20;

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.extended`](events-and-webhooks-1/events-1/event-types.md#subscription.extended)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="272">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>Description of subscription</td><td><p><code>invoice.description</code></p><p></p><p>For details, refer to <a href="../developer-resources/digital-river-api-reference/plans.md#name"><code>name</code></a> in <a href="../developer-resources/digital-river-api-reference/plans.md">Plans</a>.</p></td></tr><tr><td>The date the free trial was activated</td><td><code>subscription.stateTransitions.activatedFree</code></td></tr><tr><td>The first scheduled billing date </td><td><code>subscription.nextInvoiceDate</code></td></tr><tr><td>A description of each product in the subscription</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url</code>) in <code>invoice.items[].productDetails</code></td></tr><tr><td>The cost and quantity of each product in the subscription</td><td><code>amount</code> and <code>quantity</code> in <code>invoice.items[]</code></td></tr><tr><td>The payment method to be charged</td><td><code>invoice.payment.sources[]</code></td></tr><tr><td>Taxes to be assessed</td><td><code>invoice.totalTax</code></td></tr><tr><td>A subtotal of the amount that the customer is to be charged</td><td><code>invoice.subtotal</code></td></tr><tr><td>The total amount that the customer is to be charged</td><td><code>invoice.totalAmount</code></td></tr></tbody></table>

### Renewal reminder

This notification reminds customers that their recurring products are scheduled to renew in the near future. It should include the subscription's name and a description of its goods, the amount the customer is to be charged, and the upcoming billing date.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.reminder`](events-and-webhooks-1/events-1/event-types.md#subscription.reminder)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="277">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>Description of subscription</td><td><code>invoice.description</code><br><br>For details, refer to <a href="../developer-resources/digital-river-api-reference/plans.md#name"><code>name</code></a> in <a href="../developer-resources/digital-river-api-reference/plans.md">Plans</a>.</td></tr><tr><td>Start date of subscription</td><td><code>subscription.stateTransitions.activated</code></td></tr><tr><td>The next scheduled billing date</td><td><code>subscription.nextInvoiceDate</code></td></tr><tr><td>A description of each product in the subscription</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url</code>) in <code>invoice.items[].productDetails</code></td></tr><tr><td>The cost and quantity of each product in the subscription</td><td><code>amount</code> and <code>quantity</code> in <code>invoice.items[]</code></td></tr><tr><td>Payment method to be charged</td><td><code>invoice.payment.sources[]</code></td></tr><tr><td>Taxes to be assessed</td><td><code>invoice.totalTax</code></td></tr><tr><td>A subtotal of the amount that the customer is to be charged</td><td><code>invoice.subtotal</code></td></tr><tr><td>The total amount that the customer is to be charged</td><td><code>invoice.totalAmount</code></td></tr></tbody></table>

### Renewal confirmation

This notification informs customers that their subscription has renewed and its designated payment method was successfully charged.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.extended`](events-and-webhooks-1/events-1/event-types.md#subscription.extended)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="276">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The order identifier</td><td><code>invoice.orderId</code></td></tr><tr><td>Description of subscription</td><td><code>invoice.description</code><br><br>For details, refer to <a href="../developer-resources/digital-river-api-reference/plans.md#name"><code>name</code></a> in <a href="../developer-resources/digital-river-api-reference/plans.md">Plans</a>.</td></tr><tr><td>Start date of subscription</td><td><code>subscription.stateTransitions.activated</code></td></tr><tr><td>A description of each product in the subscription</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url</code>) in <code>invoice.items[].productDetails</code></td></tr><tr><td>The cost and quantity of each product in the subscription</td><td><code>amount</code> and <code>quantity</code> in <code>invoice.items[]</code></td></tr><tr><td>The payment method that was charged</td><td><code>invoice.payment.sources[]</code></td></tr><tr><td>Assessed taxes</td><td><code>invoice.totalTax</code></td></tr><tr><td>Applied discounts</td><td><code>invoice.totalDiscount</code></td></tr><tr><td>A subtotal of the amount charged</td><td><code>invoice.subtotal</code></td></tr><tr><td>The total amount charged</td><td><code>invoice.totalAmount</code></td></tr><tr><td>Next scheduled billing date </td><td><code>subscription.nextInvoiceDate</code></td></tr></tbody></table>

### Subscription cancelled notification

This notification informs customers that their request to cancel a subscription has been successfully processed. It should ideally contain details on the cancelled products.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.updated`](events-and-webhooks-1/events-1/event-types.md#subscription.updated)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="282">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The effective cancellation date</td><td><code>stateTransitions.cancelled</code></td></tr><tr><td>A description of each cancelled subscription product</td><td><code>items[].skuId</code><br><br>To access product details, use this identifier to <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/retrieveSkus">retrieve the SKU</a>.</td></tr></tbody></table>

### Updated terms

This notification informs customers of an update to their subscription's terms and conditions. It should describe the upcoming changes and, in the event that customers don't agree with them, provide a way for them to cancel the subscription.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.updated`](events-and-webhooks-1/events-1/event-types.md#subscription.updated)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="282">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>The updated terms</td><td><code>planId</code><br><br>To access the updated terms and conditions, use this identifier to <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans/operation/retrievePlans">retrieve the plan</a>.</td></tr><tr><td>A description of each product in the description</td><td><code>items[].skuId</code><br><br>To access product details, use this identifier to <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/retrieveSkus">retrieve the SKU</a>.</td></tr></tbody></table>

### Billing failed notification

This notification informs customers that an unsuccessful attempt was made to charge the payment method funding their subscription. To avoid losing access to their recurring products, the message should contain instructions on how customer's can update or replace this payment method.

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.payment_failed`](events-and-webhooks-1/events-1/event-types.md#subscription.payment\_failed)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="286">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>Description of subscription</td><td><code>invoice.description</code><br><br>For details, refer to <a href="../developer-resources/digital-river-api-reference/plans.md#name"><code>name</code></a> in <a href="../developer-resources/digital-river-api-reference/plans.md">Plans</a>.</td></tr><tr><td>Payment method that could not be charged</td><td><code>invoice.payment.sources[]</code></td></tr><tr><td>The number of unsuccessful billing attempts that have been made so far</td><td><code>invoice.attemptCount</code></td></tr><tr><td>A description of the products that customers will lose access to unless they take action</td><td><code>name</code>, (and optionally <code>description</code>, <code>image</code>, and <code>url</code>) in <code>invoice.items[].productDetails</code></td></tr></tbody></table>

### Subscription failed notification

This message informs customers that their subscription has been deactivated because payment couldn't be collected during the designated billing period. It's recommended that you include instructions on how customers can reactivate their subscription.&#x20;

**Recommended** [**`type`**](events-and-webhooks-1/events-1/#event-types) **of** [**triggering event**](customer-notifications.md#triggering-events): [`subscription.failed`](events-and-webhooks-1/events-1/event-types.md#subscription.failed)

Use the following table to learn which attributes in the [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) [`data.object`](events-and-webhooks-1/events-1/#event-data) contain values that can be used to populate the notification.

<table><thead><tr><th width="286">Notification information</th><th>Relevant attribute</th></tr></thead><tbody><tr><td>Description of failed subscription</td><td><code>planId</code><br><br>Use this identifier to <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans/operation/retrievePlans">retrieve the plan</a> and access description information. For details, refer to <a href="../developer-resources/digital-river-api-reference/plans.md#name"><code>name</code></a> in <a href="../developer-resources/digital-river-api-reference/plans.md">Plans</a>. </td></tr><tr><td>Description of products in failed subscription</td><td><code>items[].skuId</code><br><br>To access product details, use this identifier to <a href="https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/retrieveSkus">retrieve the SKU</a>.</td></tr><tr><td>The date that the subscription failed</td><td><code>stateTransitions.failed</code></td></tr></tbody></table>

### Payment method expiration

Prior to a subscription's renewal, this message informs customers that the designated payment method has either expired or will expire before the scheduled renewal date. The notification should provide customers a way to either update the subscription's current payment method or replace it with a new one.&#x20;

In the Digital River APIs, no [events](events-and-webhooks-1/events-1/) currently exist that can be used to trigger this notification.
