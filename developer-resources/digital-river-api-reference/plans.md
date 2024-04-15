---
description: Learn more about the plans resource
---

# Plans

On this page, you'll find information on:

* [The plans resource](plans.md#the-plans-resource)
* [The lifecycle of a plan](plans.md#lifecycle-of-a-plan)

## The plans resource

[Plans](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) define the recurring billing behavior of a group of [subscriptions](subscriptions.md). Since plans can be used to perform reporting and bulk operations, you should be careful when adding different subscription products to the same plan.

For complete specifications, refer to the [Plans API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) reference documentation.

### Identifier

When [creating a plan](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createPlans), you can specify its `id` . The value cannot contain whitespaces. If you don't provide an `id`, Digital River generates a [UUID](https://en.wikipedia.org/wiki/Universally\_unique\_identifier).

### Name

A [plan's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) `name` should describe the [subscription](subscriptions.md) products that belong to it. We recommend that you select a `name` specific enough for inclusion in [customer notifications](../../order-management/customer-notifications.md). When Digital River creates a [draft invoice](../../integration-options/checkouts/subscriptions/invoices.md#the-invoice-lifecycle) at the start of each billing cycle, we use the plan's `name` to set the [invoice's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) `description` . We then add `invoice.description` to the [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with the [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`subscription.extended`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.extended), [`subscription.payment_failed`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.payment\_failed), and [`subscription.reminder`](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.reminder).

### Terms

A [plan's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) `terms` should contain the contractual agreement displayed to customers during the acquisition process. These `terms` define the subscription, provide links to Digital River's [terms of sale](https://store.digitalriver.com/store/defaults/en\_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc.) and [privacy policy](https://store.digitalriver.com/store/defaults/en\_US/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Inc.), and stipulate that customers agree to store their payment information for use in renewals.

These should be the same [terms displayed to customers](../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#displaying-terms-and-acquiring-consent) during the acquisition process.

### Contract length and billing intervals <a href="#contract-length-and-interval" id="contract-length-and-interval"></a>

The optional `contractBindingDays` indicates the agreed upon length of the contract. For example, an annual subscription should have a value of `365`.

The data in this field is used only for compliance and transparency purposes. Therefore, your integration must be set up to allow customers to [cancel subscriptions](../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#cancelling-a-subscription) after the designated period elapses. Of course, during this contract period, you can always grant customers an exemption and allow them to cancel their subscriptions.

The billing `interval` is used in combination with the `intervalCount`. You can set up plans with intervals of `day`, `week`, `month` or `year`. The `intervalCount` is how often the customer is billed per the unit of time specified by `interval`. The `intervalCount` must be `1` or greater and cannot exceed `1000`.

The following examples demonstrate the relationship between these variables:

{% tabs %}
{% tab title="Example one" %}
This defines a subscription with a binding length of one year. The customer is billed annually.

```javascript
{
    ...
    "contractBindingDays": 365,
    "interval": "year",
    "intervalCount": 1,
    ...
}
```
{% endtab %}

{% tab title="Example two" %}
This defines a subscription with a binding length of one year. The customer is billed every six months.

```javascript
{
    ...
    "contractBindingDays": 365,
    "interval": "month",
    "intervalCount": 6,
    ...
}
```
{% endtab %}

{% tab title="Example three" %}
This defines a subscription with a binding length of one month. The customer is billed every two weeks.

```javascript
{
    ...
    "contractBindingDays": 30,
    "interval": "week",
    "intervalCount": 2,
   ...
}
```
{% endtab %}
{% endtabs %}

### Billing offset days <a href="#billing-offset" id="billing-offset"></a>

The `billingOffsetDays` represents how many days before the end of the billing period that Digital River [opens an invoice](../../integration-options/checkouts/subscriptions/invoices.md#invoice-states). For example, if you want Digital River to start attempting to capture payment ten days before the billing period ends, set this parameter to `10`.

The `billingOffsetDays` cannot be greater than the [`collectionPeriodDays`](plans.md#collection-period-days). Such a configuration could potentially result in the billing process concluding without a successful payment capture but with time still remaining in the current cycle.

{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "collectionPeriodDays",
            "message": "billingOffsetDays cannot be greater than collectionPeriodDays."
        }
    ]
}
```
{% endcode %}

### Renewal reminder days <a href="#renewal-reminders" id="renewal-reminders"></a>

The `reminderOffsetDays` represents the number of days prior to the initiation of billing that Digital River sends you the [renewal reminder event](../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.reminder). This event should trigger a corresponding event in your system that sends a reminder to the customer.

For example, if you want to set up your system to email a customer one week before Digital River [opens an invoice](../../integration-options/checkouts/subscriptions/invoices.md#invoice-states), set `reminderOffsetDays` to `7`.

The `reminderOffsetDays` cannot be greater than the [`contractBindingDays`](plans.md#contract-length-and-interval).

### Collection period days

The `collectionPeriodDays` represents the number of days that Digital River attempts to collect payment. If you set this parameter to `0` or `1` , we make a single attempt to bill the customer. But if you provide a value greater than `1`, and the first billing attempt fails, our [smart autorenewal service](../../integration-options/checkouts/subscriptions/invoices.md#invoice-billing) continues making collection attempts for the number of days you specify.

### Billing optimization

Once a plan is created, `billingOptimization` indicates whether our [smart autorenewal service](../../integration-options/checkouts/subscriptions/invoices.md#billing-optimization) is activated for that plan's subscriptions.

### State

For more information on the `state` attribute, refer to the [lifecycle of a plan](plans.md#lifecycle-of-a-plan) section.

## Lifecycle of a plan

[Plans](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) can be created in a `draft` or `active` state. But [subscriptions](subscriptions.md) can only be added to `active` plans. In other words, once you [activate a plan](../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#creating-and-activating-plans), Digital River accepts its identifier when you create a subscription.

After a plan is `discontinued`, any subscriptions currently on that plan continue renewing. You cannot, however, add any new subscriptions to a `discontinued` plan.

When a plan is `deactivated`, any subscriptions currently on that plan become [`ended`](subscriptions.md#lifecycle-of-a-subscription) on their [`nextInvoiceDate`](subscriptions.md#state) and any new subscriptions that you attempt to add are blocked.

For details, refer to [discontinuing and deactivating plans](../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#discontinuing-and-deactivating-plans).

The only two states that allow a plan's subscriptions to continue billing are `active` and `discontinued`.

![](<../../.gitbook/assets/Plans lifecycle.png>)
