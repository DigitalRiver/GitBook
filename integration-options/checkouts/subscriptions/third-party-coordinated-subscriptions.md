---
description: >-
  Gain a better understanding of how to do acquisitions and manage recurring
  billing with a third-party subscription service
---

# Handling external subscription acquisitions

If you're not using [our subscription service](../../../using-our-services/subscriptions.md), you can still use the Digital River APIs and [DigitalRiver.js](../../../payments/payment-integrations-1/digitalriver.js/reference/) to handle recurring billing, display and acquire acceptance of a subscription's terms, and comply with [PSD2 and SCA](../../../payments/psd2-and-sca/) mandates.

Integrations that use a third-party subscription service can:

* Supply an upstream [subscription identifier](subscription-information-1.md#subscription-identifier)
* Use [billing agreements](subscription-information-1.md#billing-agreements) to maintain SCA compliance
* Flag a subscription as a [free trial](subscription-information-1.md#free-trial)
* Use the [auto renewal flag](subscription-information-1.md#auto-renewal) to ensure that appropriate payment methods are displayed
* Persist a subscription's [terms and conditions](subscription-information-1.md#terms)
* Specify a subscription's [start time and end time](subscription-information-1.md#start-and-end-time).

## Building a subscription acquisition

During subscription acquisitions, you need to:

* [Configure the checkout](third-party-coordinated-subscriptions.md#configure-the-checkout)
* [Acquire acceptance of the autorenewal terms](third-party-coordinated-subscriptions.md#handling-the-autorenewal-terms)
* [Handle the subscription's payment](third-party-coordinated-subscriptions.md#handling-payments)
* [Submit the payment authorization request](third-party-coordinated-subscriptions.md#submitting-the-acquisition-authorization-request)
* [Notify customers of the acquisition](third-party-coordinated-subscriptions.md#notifying-customers-of-a-subscription-acquisition)

### Configure the checkout

Prior to [order creation](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), a subscription acquisition [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) must contain:

* A `customerId` that references an existing [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers)
* A [primary payment `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) that is [reusable ](../../../payments/payment-sources/#reusable-or-single-use)and saved to the referenced [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers)
* A [`chargeType`](../creating-checkouts/initiating-a-charge.md) that is [`customer_initiated`](../creating-checkouts/initiating-a-charge.md#customer-initiated), thereby indicating that the customer is an active participant in the acquisition process.

In addition, each [`items[]`](../creating-checkouts/describing-the-items/) in the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) that has [`subscriptionInfo`](subscription-information-1.md):&#x20;

* Can use [SKUs](../../../product-management/skus.md#skus) or [`productDetails`](../../../product-management/skus.md#product-details) to represent a [digital or physical product](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital)&#x20;
* Must set [`autoRenewal`](subscription-information-1.md#auto-renewal) to `true`
* Must contain the subscription's [`terms`](subscription-information-1.md#terms)

{% tabs %}
{% tab title="Checkout" %}
```
{
    "id": "7e5e832a-0c78-43e1-b136-ced8c156f5b8",
    "createdTime": "2022-04-07T20:49:49Z",
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
            "id": "e782d614-1444-4e37-a103-d9726288e0ce",
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
                "terms": "Subscription terms accepted by the customer",
                "autoRenewal": true,
                "freeTrial": false
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            }
        }
    ],
    "updatedTime": "2022-04-07T20:49:49Z",
    "locale": "en_US",
    "customerType": "individual",
    "chargeType": "customer_initiated",
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
            "id": "965db940-51f6-4f53-bc07-1052ef0d4c32",
            "amountContributed": 10.0,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "965db940-51f6-4f53-bc07-1052ef0d4c32_f9eae301-588a-409c-9d29-3358f19dca4f"
        }
    }
}
```
{% endtab %}
{% endtabs %}

### Acquiring acceptance of the autorenewal terms <a href="#handling-the-autorenewal-terms" id="handling-the-autorenewal-terms"></a>

During acquisitions, you must disclose a subscription's terms and then acquire the customer's active acceptance of them. How you do this depends on whether you're using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [DigitalRiver.js with Elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).

{% hint style="info" %}
For more details on required disclosures, refer to the [Subscriptions and Auto-Renewal Considerations](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=23d0d88adb5c341046e8d6aa489619ae) article (refer to [Learning tools](../../../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) for access information).
{% endhint %}

{% tabs %}
{% tab title="Drop-in payments" %}
In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), set each subscription line item's [`autoRenewal`](subscription-information-1.md#auto-renewal) to `true`. In the [`createDropin()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in) method's configuration [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options-1), set [`showTermsOfSaleDisclosure`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-terms-of-sale-disclosure) to `true`.

These settings prompt [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) to display the combined autorenewal and save payment agreement.

If customers click the [configurable continue button](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) without agreeing to the terms, Drop-in prevents the transaction from proceeding.

![](<../../../.gitbook/assets/image (83).png>)

If the customer consents and a [source](../../../payments/payment-sources/) is successfully created, then the [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event's `data` contains the agreed-upon terms (`mandate.terms`) and the time the customer accepted those terms (`mandate.signedTime`).
{% endtab %}

{% tab title="DigitalRiver.js" %}
If you're using DigitalRiver.js, you can present our standardized subscription terms and save payment agreement by calling the [get compliance details method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale), retrieving `autorenewalPlanTerms.localizedText` and then displaying that text with an appropriate acceptance control. Your code should be written so that customers must accept these terms before the checkout can proceed.

You should then pass `autorenewalPlanTerms.localizedText` to `mandate.terms` in the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object.
{% endtab %}
{% endtabs %}

If you configure your workflow correctly, then the customer accepted autorenewal terms are returned in the [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event's `data` or the response to the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method.

In either case, retrieve `mandate.terms` and use this value to set each of the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`items[].subscriptionInfo.terms`](subscription-information-1.md#terms). This ensures that the subscription's terms are added to the [billing agreement](subscription-information-1.md#billing-agreement-identifier).

### Handling payments

To fund a recurring transaction, customers can either create a new [source](../../../payments/payment-sources/) or authenticate a saved source.

For details, refer to the [subscription section](../building-you-workflows/#subscription) on the[ Building payments workflows](../building-you-workflows/) page.

### Submitting the acquisition authorization request

Once the checkout's [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state) is [`requires_confirmation`](../creating-checkouts/payment-sessions.md#requires\_confirmation), and all [address requirements](../creating-checkouts/providing-address-information.md#address-requirements-and-validations) are met, [submit the create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). At that point, Digital River generates a [billing agreement](subscription-information-1.md#billing-agreement-identifier) and returns its `billingAgreementId` in the response.

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "188817490336",
    "customerId": "533134230336",
    ...
    "items": [
        {
            "id": "110359190336",
            "skuId": "0181a7a9-610e-48c5-89e5-84ca06c69f03",
            ...
            "subscriptionInfo": {
                "terms": "Subscription terms accepted by the customer",
                "autoRenewal": true,
                "freeTrial": false,
                "billingAgreementId": "c567f049-9ec4-4c63-829b-efe01427a8a9"
            },
            ...
        }
    ],
    ...
    "state": "accepted",
    ...
    "checkoutId": "50a72152-4a61-4e4a-b9e1-2ab5db891105"
}
```
{% endtab %}
{% endtabs %}

### Notifying customers of a subscription acquisition

When the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events) is [`accepted`](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders), notify customers that their subscription acquisition has been successfully processed. In the [Subscription Notifications](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=785fc80adbd8341046e8d6aa48961907) article (_refer to_ [_Learning tools_](../../../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) _for access information_), you can find a complete list of what is required in this notification.‌

## Next steps

For details on auto-renewals and updates, refer to [Managing an external subscription](../../../subscription-management/managing-an-external-subscription.md).
