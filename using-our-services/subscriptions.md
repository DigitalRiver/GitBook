---
description: >-
  Gain a better understanding of Digital River's subscription service along with
  how to define a business model and set up free trials
---

# Subscriptions

Digital River offers a [PSD2 and SCA](../payments/psd2-and-sca/)-compliant subscription management service that automatically schedules and processes recurring payments. The service gives you the ability to offer customers free trials as well as numerous ways to fund recurring transactions.

On this page, you'll find information on:

* [How to define a business model](subscriptions.md#defining-a-business-model)
* [How to configure plans for free trials](subscriptions.md#setting-up-free-trials)
* [Payment methods that can be used to fund subscriptions](subscriptions.md#supported-payment-methods-with-subscriptions)

How you do subscription acquisitions depends on the checkout solution(s) you've selected. Use the following table to access the appropriate article:

| Checkout solution                                                | Article                                                                                                                         |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [Low-code checkouts](../integration-options/low-code-checkouts/) | [Processing subscription acquisitions](../integration-options/low-code-checkouts/processing-subscription-acquisitions.md)       |
| [Direct Integrations](../integration-options/checkouts/)         | [Handling subscription acquisitions](../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md) |

Once the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) that contains the [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) is created, you'll also need to activate the subscription, fulfill the goods, and manage renewals. For details on how to handle these, and other processes, refer to the [Managing a subscription](../subscription-management/managing-a-subscription.md) page.&#x20;

## Defining a business model

In the subscription service, [digital products](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) can be shared among [plans](../developer-resources/digital-river-api-reference/plans.md). We recommend not relying on [SKUs](../product-management/skus.md) to model subscription entitlements. We also suggest using different plans for your offerings since they can be used to model cohorts for reporting purposes.

Digital River's subscription service models recurring billing. It's not intended to model subscription access or entitlements. As a result, you cannot call the service to determine a customer's current access level.

Subscription metadata and client data linked to the subscription are useful for modeling details that are irrelevant to Digital River and within the plan's terms.

### Setting up subscription-based products

With Digital River's subscription service, you can either use [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs) or [`productDetails`](../product-management/skus.md#product-details) to define the [basic and compliance data](../product-management/skus.md#basic-versus-compliance-product-data) of any [digital product](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) that you intend to offer on a subscription-basis.

For more details, refer to [Managing SKUs](../product-management/creating-and-updating-skus.md) and [Using product details](../product-management/using-product-details.md).

### Defining plans

Once you've [built a product catalog](subscriptions.md#setting-up-subscription-based-products), you should set up [plans](../developer-resources/digital-river-api-reference/plans.md) that define the behavior of your [subscriptions](../developer-resources/digital-river-api-reference/subscriptions.md).

At a minimum, you should specify a plan's [name](../developer-resources/digital-river-api-reference/plans.md#name) and terms, designate its [contract length and billing frequency](../developer-resources/digital-river-api-reference/plans.md#contract-length-and-interval), set up [renewal reminders](../developer-resources/digital-river-api-reference/plans.md#renewal-reminders), and configure its [billing offset days](../developer-resources/digital-river-api-reference/plans.md#billing-offset) and [collection period days](../developer-resources/digital-river-api-reference/plans.md#collection-period-days).

The following diagram shows how plans define the behavior of subscriptions that belong to them.

<figure><img src="../.gitbook/assets/Subs timeline (2).png" alt=""><figcaption></figcaption></figure>

### Creating and activating plans

In a [`POST /plans`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createPlans) request, you can set `state` to `draft` or `active`. If you're using Digital River as the system of record prior to deployment, you may decide its beneficial to create `draft` plans. If you don't specify a unique `id` in the create plan request, we generate one for you.

```
curl --location --request POST 'https://api.digitalriver.com/plans' \
...
--data-raw '{
    "name": "Example Plan",
    "terms": "These are the terms...",
    "contractBindingDays": 365,
    "interval": "year",
    "intervalCount": 1,
    "reminderOffsetDays": 30,
    "billingOffsetDays": 5,
    "collectionPeriodDays":30,
    "state": "draft"
}'
```

A `201 Created` response contains a unique plan identifier. The request also triggers an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../order-management/events-and-webhooks-1/events-1/#event-types) of `plan.created`. If the [plan's](../developer-resources/digital-river-api-reference/plans.md) `state` is `draft` when you're ready to launch, send its identifier as a path parameter in a [`POST /plans/{planId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updatePlans) and use the request's body to set `state` to `active`.

```
curl --location --request POST 'https://api.digitalriver.com/plans/173577b2-6edc-4f68-9297-7f7bc2ca6e58' \
...
--data-raw '{
    "state": "active"
}'
```

The plan must be `active` before you can add [subscriptions](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) to it. For details, refer to [lifecycle of a plan](../developer-resources/digital-river-api-reference/plans.md#lifecycle-of-a-plan) and [lifecycle of a subscription](../developer-resources/digital-river-api-reference/subscriptions.md#lifecycle-of-a-subscription).

### Discontinuing and deactivating plans

Subscriptions on discontinued plans continue renewing. Deactivating a plan, however, terminates all of its active subscriptions on their [`nextInvoiceDate`](../developer-resources/digital-river-api-reference/subscriptions.md#date-of-next-invoice).

When you want to discontinue or deactivate a plan, specify the desired `state` in the payload of a [`POST /plans/{planId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updatePlans) request.

{% tabs %}
{% tab title="Discontinue" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/plans/173577b2-6edc-4f68-9297-7f7bc2ca6e58' \
...
--data-raw '{
    "state": "discontinued"
}'
```
{% endtab %}

{% tab title="Deactivate" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/plans/173577b2-6edc-4f68-9297-7f7bc2ca6e58' \
...
--data-raw '{
    "state": "deactivated"
}'
```
{% endtab %}
{% endtabs %}

If you attempt to create subscriptions that belong to `discontinued` or `deactivated` plans, an error is thrown during the acquisition checkout.

{% tabs %}
{% tab title="400 Bad Request" %}
```
{
    "type": "bad_request",
    "errors": [
        {
            "code": "plan_not_active",
            "parameter": "planId",
            "message": "Plan 86a05e42-3b94-4ee5-b2a5-267efd8b3704 is not active."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

For details on how discontinuing or deactivating a plan affects its associated subscriptions, refer to [lifecycle of a plan](../developer-resources/digital-river-api-reference/plans.md#lifecycle-of-a-plan) and [lifecycle of a subscription](../developer-resources/digital-river-api-reference/subscriptions.md#lifecycle-of-a-subscription).

## Setting up free trials

You can configure a customer's subscription so that it starts with a free trial period. In this section, you'll find information on [defining trial and paid plans](subscriptions.md#defining-trial-and-paid-plans) prior to deployment.\
\
How you handle subscription acquisitions that involve free trials depends on the checkout solution(s) you've selected. Use the following table to access the relevant content:

| Checkout solution                                                                  | Article                                                                                                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Prebuilt Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md) | [Trial subscription acquisitions](../integration-options/low-code-checkouts/processing-subscription-acquisitions.md#managing-trial-subscription-acquisitions) in [Processing subscription acquisitions](../integration-options/low-code-checkouts/processing-subscription-acquisitions.md)               |
| [Direct Integrations](../integration-options/checkouts/)                           | [Trial subscription acquisitions](../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#managing-trial-subscription-acquisitions) in [Handling subscription acquisitions](../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md) |

Once the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) that contains the [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) is created, you'll also need to convert the subscription from trial to paid. For details, refer to [Trial subscription management](../subscription-management/managing-a-subscription.md#trial-subscription-management) on the [Subscription management](../subscription-management/managing-a-subscription.md) page.&#x20;

### Defining trial and paid plans

If you'd like to offer free trials, prior to deployment you'll need to configure [plans](../developer-resources/digital-river-api-reference/plans.md) for your trial [subscriptions](../developer-resources/digital-river-api-reference/subscriptions.md).

{% hint style="success" %}
For general information on plans and their relationship to subscriptions, refer to [Defining plans](subscriptions.md#defining-plans).
{% endhint %}

For each subscription you intend to offer on a trial basis, you should define a [trial period plan](subscriptions.md#trial-period-plans) and a [paid period plan](subscriptions.md#paid-period-plans). The following diagram shows how you might set up two plans that result in a seven-day free trial period followed by a monthly, recurring billing cycle:

<div align="left">

<img src="../.gitbook/assets/Free trial.png" alt="">

</div>

#### Trial period plans

Your trial period [plan](../developer-resources/digital-river-api-reference/plans.md) controls the [subscription's](../developer-resources/digital-river-api-reference/subscriptions.md) behavior during its first billing cycle.

The plan's `interval` and `intervalCount` determine the trial period's length. If, for example, you want to offer a 31-day free trial period, set `interval` to `day` and `intervalCount` to `31` .

For free trial plans, set `billingOffsetDays` to `0`. This configuration results in a subscription whose initial billing cycle has the same [`nextInvoiceDate`](../developer-resources/digital-river-api-reference/subscriptions.md#date-of-next-invoice) and [`currentPeriodEndDate`](../developer-resources/digital-river-api-reference/subscriptions.md#current-period-end-date), thereby ensuring that the first payment capture attempt occurs after the trial period ends.

The value you give `reminderOffsetDays` determines when the [`subscription.reminder`](../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.reminder) event is created. For example, a `reminderOffsetDays` of `3` results in the creation of a `subscription.reminder` event three days before the trial period's conclusion.

Use `collectionPeriodDays` to define the number of days Digital River should attempt to capture payment. Once the trial period ends, Digital River will initially attempt to charge the customer's designated [payment source](../payments/payment-sources/). If this proves unsuccessful, our [billing optimization service](../developer-resources/digital-river-api-reference/invoices.md#billing-optimization) will continue making capture attempts for the number of days you specify.

{% code title="Plan" %}
```javascript
{
    "id": "186cf07e-a1ea-4ec0-9d9a-8aa93b3af43a",
    "createdTime": "2022-02-11T14:41:43Z",
    "updatedTime": "2022-02-11T14:41:43Z",
    "terms": "7-day free trial plan terms",
    "contractBindingDays": 7,
    "interval": "day",
    "intervalCount": 7,
    "name": "7-day SaaS free trial",
    "billingOptimization": true,
    "billingOffsetDays": 0,
    "collectionPeriodDays": 4,
    "reminderOffsetDays": 3,
    "state": "active",
    "stateTransitions": {
        "activated": "2022-02-11T14:41:43Z"
    },
    "liveMode": false
}
```
{% endcode %}

#### Paid period plans

You must also define a paid period [plan](../developer-resources/digital-river-api-reference/plans.md) that governs the [subscription](../developer-resources/digital-river-api-reference/subscriptions.md) after its trial conversion. On the following plan, customers are billed monthly, and in every billing cycle, Digital River makes the first payment capture attempt three days before the end period date.

{% code title="Plan" %}
```javascript
{
    "id": "f55d07a2-a78f-406a-b6c6-ad8e1cc1531b",
    "createdTime": "2022-02-11T14:42:53Z",
    "updatedTime": "2022-02-11T14:42:53Z",
    "terms": "The terms of a one-year plan that is billed monthly",
    "contractBindingDays": 365,
    "interval": "month",
    "intervalCount": 1,
    "name": "SaaS monthly billing plan",
    "billingOptimization": true,
    "billingOffsetDays": 3,
    "collectionPeriodDays": 7,
    "reminderOffsetDays": 4,
    "state": "active",
    "stateTransitions": {
        "activated": "2022-02-11T14:42:53Z"
    },
    "liveMode": false
}
```
{% endcode %}

## **Supported payment methods with subscriptions**

When setting up payment in acquisitions or modifying a subscription's payment source, customers must select from payment methods that can be used in recurring transactions.

For a complete list of such payment methods, refer to the [Supported payment methods](../payments/supported-payment-methods/) page.

{% hint style="success" %}
In acquisition checkouts, you can combine a [reusable](../payments/payment-sources/#reusable-or-single-use) primary source with one or more secondary sources. For details, refer to [combining primary and secondary payment sources](../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](../payments/payment-sources/using-the-source-identifier.md) page.
{% endhint %}

## Next steps

To learn more about how you interact with subscriptions during checkouts, use the following table to access the appropriate article:&#x20;

| Checkout solution                                                | Article                                                                                                                         |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [Low-code checkouts](../integration-options/low-code-checkouts/) | [Processing subscription acquisitions](../integration-options/low-code-checkouts/processing-subscription-acquisitions.md)       |
| [Direct Integrations](../integration-options/checkouts/)         | [Handling subscription acquisitions](../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md) |

