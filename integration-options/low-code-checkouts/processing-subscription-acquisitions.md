---
description: >-
  Gain a better understanding of how to use Digital River's subscription service
  to process acquisitions in Prebuilt Checkout and Components
---

# Processing subscription acquisitions

If you're pairing either of Digital River's [low-code checkout solutions](./) with [our subscription service](../../using-our-services/subscriptions.md), this page explains how to process:

* [Standard subscription acquisitions](processing-subscription-acquisitions.md#building-acquisitions)
* [Trial subscription acquisitions](processing-subscription-acquisitions.md#managing-trial-subscription-acquisitions)

Once Digital River converts the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), you'll also need to activate the subscription, fulfill the goods, and manage renewals. For details on how to handle these, and other processes, refer to the [Managing a subscription ](../../subscription-management/managing-a-subscription.md)page.

## Subscription acquisitions <a href="#building-acquisitions" id="building-acquisitions"></a>

During a standard subscription acquisition, your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) must pass `subscriptionInfo` in `items[]`.&#x20;

For each `items[].subscriptionInfo` in the request:

* Use `planId` to associate the [subscription](../../developer-resources/digital-river-api-reference/subscriptions.md) with a [plan](../../developer-resources/digital-river-api-reference/plans.md). For details, refer to [Defining a business model](../../using-our-services/subscriptions.md#defining-a-business-model).
* Include `terms`. To do this, prior to submitting the request, [get the plan that the subscription belongs to](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans). From the response, retrieve the [plan's](../../developer-resources/digital-river-api-reference/plans.md) `terms` and pass that value in the request. \
  \
  If you don't pass `terms`, a `400 Bad Request` with a `code` of `missing_parameter` is returned.
* Set `autoRenewal` to `true` or omit the value. If you set this parameter to `false`, a `400 Bad Request` with a `code` of `invalid_request` is returned.
* If you don't provide a unique `subscriptionId`, we generate one for you.

Your request must also pass a [`customerId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-identifier) and should specify a `chargeType` of `customer_initiated`.

Acquisition requests can also contain:

* [Multiple `items[]` with `subscriptionInfo`](processing-subscription-acquisitions.md#subscriptions-with-multiple-line-items)
* [A mix of both subscription and non-subscription `items[]`](processing-subscription-acquisitions.md#mixed-carts)

#### Multiple `items[]` with `subscriptionInfo` <a href="#subscriptions-with-multiple-line-items" id="subscriptions-with-multiple-line-items"></a>

Your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) can contain multiple `items[]` with `subscriptionInfo`. However, all these recurring `items[]` have to share the same `planId` and (if you pass your own value) `subscriptionId`.&#x20;

If your request contains multiple `items[]` with `subscriptionInfo` and they reference different [plans](../../developer-resources/digital-river-api-reference/plans.md), then the following error is returned:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "plan_limit_reached",
            "parameter": "planId",
            "message": "Only one unique subscription plan can be supported in a checkout"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

#### Mixed subscription and non-subscription `items[]` <a href="#mixed-carts" id="mixed-carts"></a>

Your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) can also have a mix of `items[]`, some with and some without `subscriptionInfo`. This allows you to, for example, process transactions that combine the purchase of a one-time physical product with a recurring digital subscription.

## Trial subscription acquisitions <a href="#managing-trial-subscription-acquisitions" id="managing-trial-subscription-acquisitions"></a>

You handle free-trial acquisitions in much the same way as [standard subscription acquisitions](processing-subscription-acquisitions.md#building-acquisitions).&#x20;

However, in free trials, you must slightly modify your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).

For each trial-based `items[]` in the request:

* Pass a `price` or `aggregatePrice` of `0.0`
* In its `subscriptionInfo`:
  * Set `freeTrial` to `true`
  * Pass a `planId` that references a [trial period plan](../../using-our-services/subscriptions.md#trial-period-plans).

If your request contains an `items[]` whose (1) `subscriptionInfo.freeTrial` is `true` and its `price` or `aggregatePrice` is greater than `0.0` or (2) whose `subscriptionInfo.freeTrial` is `false` and its `price` or `aggregatePrice` is `0.0`, then the following error is thrown:

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "items",
            "message": "The value of the Free Trial flag is not consistent with the item price or the aggregate price."
        }
    ]
}
```
{% endcode %}

For details on how to process a trial-based subscription after Digital River converts the acquisition [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), refer to [Trial subscription management](../../subscription-management/managing-a-subscription.md#trial-subscription-management) on the [Subscription management](../../subscription-management/managing-a-subscription.md) page.

## How Digital River processes your requests <a href="#handling-the-response" id="handling-the-response"></a>

For each `items[]` with `subscriptionInfo` sent in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), Digital River creates a single [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions), sets its to [`state`](../../developer-resources/digital-river-api-reference/subscriptions.md#state) to `draft` and then generates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`subscription.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.created).&#x20;

{% hint style="info" %}
The event's [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) doesn't contain [key subscription attributes](../../developer-resources/digital-river-api-reference/subscriptions.md) such as `contractBindingUntil`, `nextReminderDate`, `currentPeriodEndDate`, and `nextInvoiceDate`. These are populated after you [activate the subscription](../../subscription-management/managing-a-subscription.md#activating-a-subscription).&#x20;
{% endhint %}

Digital River also presents customers with a localized, recurring billing agreement in the payment collection stage and forces them to accept it before they can submit the order.&#x20;

{% tabs %}
{% tab title="Prebuilt Checkout" %}
{% hint style="success" %}
In [Prebuilt Checkout](drop-in-checkout.md), we retrieve the [`interval` and `intervalCount`](../../developer-resources/digital-river-api-reference/plans.md#contract-length-and-interval) of the [plan](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) that the [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) belongs to and present this information in the order summary section.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>


{% endtab %}

{% tab title="Payment Component" %}
<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

To make the [primary payment `sources[]`](../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) [reusable](../../payments/payment-sources/#reusable-or-single-use), Digital River saves it to the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) referenced by [`customerId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-identifier).&#x20;

To learn more about how to activate subscriptions and handle renewals, refer to the[ Managing a subscription](../../subscription-management/managing-a-subscription.md) page.

