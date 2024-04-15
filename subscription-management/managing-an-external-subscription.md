---
description: >-
  If you're using a third-party subscription service, gain a better
  understanding of how to submit billing  renewals and make updates
---

# Managing an external subscription

If you're not using [our subscription service](../using-our-services/subscriptions.md), you can still use the Digital River APIs manage a subscription after the [acquisition process](../integration-options/checkouts/subscriptions/third-party-coordinated-subscriptions.md) is complete. On this page, you'll find information on:

* [Auto-renewing a subscription](managing-an-external-subscription.md#auto-renewing-a-subscription)
* [Updating the subscription](managing-an-external-subscription.md#handling-subscription-changes)

## Auto-renewing a subscription

Prior to auto-renewing a subscription, you must [send the customer a reminder](managing-an-external-subscription.md#sending-the-renewal-reminder).  At the start of each new billing cycle, [configure and submit the renewal request](managing-an-external-subscription.md#configuring-the-renewal-request).  Once the renewal is successfully processed, [notify the customer](managing-an-external-subscription.md#notifying-customers-of-a-subscriptions-renewal).

### Sending the renewal reminder

For auto-renewing subscriptions that have terms greater than 30 days, you must notify the subscriber of upcoming renewals 30 days prior to the renewal date. As the renewal date approaches, we recommend you provide additional notifications.

In the [Subscription Notifications](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=785fc80adbd8341046e8d6aa48961907) article (_refer to_ [_Learning tools_](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) _for access information_), you can find a complete list of what is required in the renewal reminder.

### Configuring the renewal request

At the start of each billing cycle, build a renewal [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). Prior to [order creation](../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), a subscription renewal [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) should contain:

* A `customerId` that references the same [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) contained in the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)
* A [`sources[]`](../payments/payment-sources/) that is [reusable](../payments/payment-sources/#reusable-or-single-use), saved to the referenced [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers), and has the same `id` as the [primary source](../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) in the acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)
* A [`chargeType`](../integration-options/checkouts/creating-checkouts/initiating-a-charge.md) set to [`merchant_initiated`](../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#merchant-initiated), thereby instructing Digital River to notify payment processors that a server auto-generated the authorization request

{% hint style="warning" %}
For manual renewals, which require customers active participation, set `chargeType` to [`customer_initiated`](../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#customer-initiated) and [`autoRenewal`](../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal) to `false`.&#x20;
{% endhint %}

For each [`items[]`](../integration-options/checkouts/creating-checkouts/describing-the-items/) in the renewal [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts):

* Set [`subscriptionInfo.autoRenewal`](../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal) to `true`
* Pass the same [`subscriptionInfo.billingAgreementId`](../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreements) assigned to that item in the acquisition. Unless a [change event](managing-an-external-subscription.md#handling-subscription-changes) requires the creation of a new [billing agreement](../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreements), you should use this identifier throughout a subscription's lifecycle.‌

If an acquisition [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains multiple `items[]` with `subscriptionInfo`, and each have the same [`terms`](../integration-options/checkouts/subscriptions/subscription-information-1.md#terms), then you can process all of their renewals in the same [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). If the `terms` are different, then you should create unique [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) to renew each.

Since customers accept a subscription's terms during acquisitions, and therefore they've already been added to the billing agreement, it's not necessary to pass [`terms`](../integration-options/checkouts/subscriptions/subscription-information-1.md#terms) in the renewal request.

To authorize payment on the subscription renewal, [convert the checkout to an order](../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). A `201 Created` returns the same `billingAgreementId`, which you should continue to persist.

{% tabs %}
{% tab title="Checkout" %}
```
{
    "id": "d229fc76-3398-4038-bd90-2e152769bef0",
    "createdTime": "2022-04-07T21:42:48Z",
    "customerId": "533134230336",
    "currency": "USD",
    "email": "anyemail@digitalriver.com",
    "billTo": {
        "address": {
            "line1": "10381 Bren Rd W",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "William Brown",
        "email": "null@digitalriver.com"
    },
    "totalAmount": 10.0,
    "subtotal": 10.0,
    "totalFees": 0.0,
    "totalTax": 0.0,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "id": "39153fb7-e5d5-498f-9465-005560ba268e",
            "skuId": "0181a7a9-610e-48c5-89e5-84ca06c69f03",
            "amount": 10.0,
            "quantity": 1,
            "tax": {
                "rate": 0.0,
                "amount": 0.0
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "subscriptionInfo": {
                "autoRenewal": true,
                "freeTrial": false,
                "billingAgreementId": "c567f049-9ec4-4c63-829b-efe01427a8a9"
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            }
        }
    ],
    "updatedTime": "2022-04-07T21:42:48Z",
    "locale": "en_US",
    "customerType": "individual",
    "chargeType": "merchant_initiated",
    "sellingEntity": {
        "id": "C5_INC-ENTITY",
        "name": "DR globalTech Inc."
    },
    "liveMode": false,
    "payment": {
        "sources": [
            {
                "id": "5e359d60-1d23-4234-84ee-e1c9b3ed7edc",
                "type": "creditCard",
                "amount": 10.0,
                "owner": {
                    "firstName": "William",
                    "lastName": "Brown",
                    "email": "null@digitalriver.com",
                    "address": {
                        "line1": "10381 Bren Rd W",
                        "city": "Minnetonka",
                        "postalCode": "55343",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "creditCard": {
                    "brand": "Visa",
                    "expirationMonth": 7,
                    "expirationYear": 2027,
                    "lastFourDigits": "1111"
                }
            }
        ],
        "session": {
            "id": "e007a135-07ea-4cc8-897e-9081f3f7d9d9",
            "amountContributed": 10.0,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "e007a135-07ea-4cc8-897e-9081f3f7d9d9_51266228-527e-4add-a4e8-bac1b141ff46"
        }
    }
}
```
{% endtab %}
{% endtabs %}

### Notifying customers of a subscription's renewal

Once you either [synchronously](../order-management/creating-and-updating-an-order.md#accepted) or [asynchronously](../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) receive an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in an [`accepted`](../order-management/creating-and-updating-an-order.md#handling-accepted-orders) state, you can [fulfill](../order-management/fulfillments.md) the subscription's products, and then [capture payment](../order-management/informing-digital-river-of-a-fulfillment.md). Upon receipt of the [`order.charge.capture.complete`](../order-management/informing-digital-river-of-a-fulfillment.md#successful-charge-captures), notify end customers within 24 hours that the subscription has been renewed.

In the [Subscription Notifications](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=785fc80adbd8341046e8d6aa48961907) article (_refer to_ [_Learning tools_](../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) _for access information_), you can find a comprehensive list of the information you're required to include in this notification.

## Handling subscription updates <a href="#handling-subscription-changes" id="handling-subscription-changes"></a>

After most subscription change events, you can continue processing renewals using the same [`billingAgreementId`](../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreements) generated during the acquisition.‌

In other scenarios, when the underlying subscription is modified, we recommend that you generate a new billing agreement.

As a rule of thumb, you should create a new billing agreement whenever the scope of a subscription update is not defined in its autorenewal terms.‌

The following provides some common subscription change scenarios and indicates whether a new billing agreement is recommended.

<table data-header-hidden><thead><tr><th width="147.33333333333331"></th><th width="377"></th><th></th></tr></thead><tbody><tr><td>Scenario</td><td>Details</td><td>Same or new <code>billingAgreementId</code>?</td></tr><tr><td>Modifying payment methods</td><td><p>The payment method is updated mid-term or the customer supplies a new payment method. Two common examples are when the customer performs a mid-term <a href="../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#updating-sources">update of a credit card's expiration date</a> or, during a manual renewal, the</p><p>customer provides a credit card that is different from the one used when acquiring the subscription.</p></td><td>Same</td></tr><tr><td>Metered billing</td><td>Some subscriptions use a metered approach to billing. For example, an API subscription service might allow only a certain number of requests per month. When customers exceed that pre-defined threshold, they are charged on a per request basis, potentially causing their monthly bills to fluctuate.</td><td>Same</td></tr><tr><td>Free trials</td><td><p>After a designated period of time, it's common for free trials to convert to paid subscriptions. Unless a customer actively cancels the trial, these conversions are typically automatic.</p><p><br>As long as the acquisition agreement specifies this condition, you should continue using the same billing agreement in all post-conversion transactions.</p></td><td>Same</td></tr><tr><td>Upgrades</td><td>When you receive a customer-initiated request to upgrade the subscription to a higher service level, we recommend you generate a new billing agreement. For example, a customer currently enrolled in a $100/month plan might request an upgrade to a $200/month plan.</td><td>New</td></tr><tr><td>Modifying a subscription's billing cycle or duration</td><td>A customer requests a modification to a subscription's billing cycle or duration. For example, the customer might want to switch from monthly to annual billing.</td><td>New</td></tr><tr><td>Updating a subscription's quantity</td><td><p>This describes a customer-initiated change to the <code>quantity</code> of a subscription line item.</p><p>​</p><p>In this scenario, since Digital River's standardized autorenewal terms do not stipulate that the customer's saved payment information can be used for quantity modifications, you need to generate a new billing agreement.</p></td><td>New</td></tr><tr><td>Adding a new subscription</td><td>A customer purchases an add-on subscription product or service and the add-on requires creating a unique line item with <a href="../integration-options/checkouts/subscriptions/subscription-information-1.md">subscription information</a>.</td><td>New</td></tr></tbody></table>
