---
description: Learn about a checkout's subscription information
---

# Subscription information

As [reseller of record](../../../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor), Digital River is required to collect basic subscription data. As a result, all [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that contain recurring products or services must have `subscriptionInfo`.

A checkout's `subscriptionInfo` can be used to hold data on:

* [Auto renewals](subscription-information-1.md#auto-renewal)
* [Free trials](subscription-information-1.md#free-trial)
* [Contractual terms](subscription-information-1.md#terms)
* [Subscription identifiers](subscription-information-1.md#subscription-identifier)
* [Billing agreements identifiers](subscription-information-1.md#billing-agreements)
* [Start and end times](subscription-information-1.md#start-and-end-time)

This data, along with the [charge type](../creating-checkouts/initiating-a-charge.md), is what you'll use to set up and renew subscriptions.

If you're using [Digital River's subscription service](../../../using-our-services/subscriptions.md), we manage most of this data. For integrations that use [third party subscription services](third-party-coordinated-subscriptions.md), you must supply these details in both acquisition and renewal [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "192498520336",
    ...
    "items": [
        {
            "id": "114400500336",
            ...
            "subscriptionInfo": {
                "subscriptionId": "acf73606-a8f1-4126-8156-0467e73ae4ae",
                "terms": "Subscription terms accepted by the customer",
                "autoRenewal": true,
                "freeTrial": false,
                "billingAgreementId": "0555aec0-2c75-4306-aa2b-4d102233f1f0",
                "startTime": "2021-07-07T13:47:13Z",
                "endTime": "2022-07-07T13:47:13Z"
            },
            ...
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

For server-initiated auto-renewals, the required `subscriptionInfo` configurations are `autoRenewal` set to `true`, the `subscriptionId` that you may have provided during the acquisition and the [`billingAgreementId`](subscription-information-1.md#billing-agreements) from the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). You should also set the checkout's [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `merchant_initiated`.

## Auto renewal

The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `autoRenewal` indicates whether subscriptions renew automatically or manually. During the acquisition of auto-renewing subscriptions, customers need to actively consent to automatic recurring billing. So, when `autorenewal` is `true`, customers must agree to have their payment information stored on file and then charged at the start of every billing cycle.‌

This setting is also necessary to ensure that only [reusable payment methods](../../../payments/supported-payment-methods/) are displayed to customers.

For manual renewals, customers must be actively involved in both the acquisition and renewal process. This means that at the point of sale, customers supply payment information, which you then use to either [create a new source](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) or [authenticate an existing source](../../../payments/payment-sources/using-the-source-identifier.md#authenticating-sources).

## Free trial

When you offer customers a free trial period to evaluate a subscription, and you also collect their payment information, make sure that you set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `freeTrial` to `true`. To satisfy our [reseller of record](../../../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements, Digital River needs to know that payment details are being collected, even when no charge authorization occurs.‌

If you're using [Digital River's subscription service](../../../using-our-services/subscriptions.md) and you want to offer no-charge, trial subscriptions, `freeTrial` also needs to be `true`. For details, refer to [Trial subscription acquisitions](digital-river-coordinated-subscriptions.md#managing-trial-subscription-acquisitions).

## Terms

The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `terms` hold the subscription's contractual agreement. These should be the Digital River approved terms displayed to customers during acquisitions. Prior to creating a subscription, your integration must acquire the customer's active acceptance of them. They define the subscription, provide links to Digital River's [terms of sale](https://store.digitalriver.com/store/defaults/en\_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc.) and [privacy policy](https://store.digitalriver.com/store/defaults/en\_US/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Inc.), and stipulate that the customer agrees to store their payment information for use in renewals.

## Billing agreements

As part of the [PSD2 Strong Customer Authentication (SCA)](../../../payments/psd2-and-sca/) initiative, payment processors require extra information when handling [merchant-initiated](../creating-checkouts/initiating-a-charge.md#merchant-initiated) credit card transactions. To comply with this mandate, we make use of billing agreements.

Among other information, a billing agreement contains the [terms and conditions](subscription-information-1.md#terms) agreed to by the customer during a subscription's acquisition. This agreement demonstrates that the customer consented to have their payment information saved and then used in recurring transactions.

By connecting the customer-initiated subscription acquisition with merchant-initiated autorenewals, you stay in compliance with relevant PSD2 SCA mandates and we can make payment authorization requests that are more likely to succeed.‌

When you [convert a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), and that checkout contains a [line item](../creating-checkouts/describing-the-items/) with `subscriptionInfo`, we create a billing agreement and return its `billingAgreementId` in the `POST/orders` response.

{% hint style="info" %}
A one-to-one relationship exists between a subscription and a billing agreement. For example, if the transaction contains two line items and both have `subscriptionInfo` (i.e., both are subscriptions), then Digital River generates two separate billing agreements and returns two billing agreement identifiers.‌
{% endhint %}

If you're using [Digital River's subscription service](../../../using-our-services/subscriptions.md), we associate the billing agreement with the [subscription](digital-river-coordinated-subscriptions.md#billing-agreement-identifier) and make sure `billingAgreementId` is sent in all renewal requests. For those using a [third-party subscription service](third-party-coordinated-subscriptions.md), you need to retrieve `billingAgreementId` from the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and pass it in all renewal requests.

## Subscription identifier

The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `subscriptionId` field identifies a subscription.

If you're using [Digital River's subscription service](../../../using-our-services/subscriptions.md), you can pass your own `subscriptionId`. If you don't, we generate an identifier for you. In either case, the value uniquely identifies the [subscription](digital-river-coordinated-subscriptions.md#the-subscriptions-object) in our system.

If you're using a [third-party subscription service](third-party-coordinated-subscriptions.md), Digital River doesn't generate a `subscriptionId`. You must send your own value during the [checkout process](../creating-checkouts/). In this case, whenever you process a renewal, its best practice to provide us the same `subscriptionId` you sent during the acquisition.

## Start and end time

​To create an auto-renewing subscription using [Klarna](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/klarna.md), you must provide both a `startTime` and `endTime`. This data helps Klarna's risk engine make an accurate assessment of a transaction's validity, thereby improving conversion and acceptance rates.‌

When defining `startTime` and `endTime`, make sure you adhere to the [date/time standard used in the Digital River APIs](../../../developer-resources/api-structure.md#dates-and-times). If either value is improperly formatted, you receive a `400 Bad Request` with an error `code` of `invalid_parameter`.

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "endTime",
            "message": "2021-06-07T13:47:13Zxyxy is not a valid timestamp."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

During acquisitions, specify `startTime` as the current date. The `endTime` should be the `startTime` + the subscription duration, also known as the payment schedule. The payment schedule is how often customers pay for their subscription. As an example, customers might have a year-long subscription that they pay monthly. We treat the subscription duration and payment schedule as equivalent.‌

For example, if the `startTime` of an annually billed subscription is `2021-07-07T13:47:13Z` then set `endTime` to `2022-07-07T13:47:12Z`. For a monthly recurring subscription with the same `startTime`, you would set `endTime` to `2021-08-07T13:47:12Z`.‌

To renew an open-ended subscription that bills monthly, [build a checkout](../creating-checkouts/) and [convert that checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) on a monthly basis, updating `startDate` and `endDate` in each request, until the customer cancels.‌
