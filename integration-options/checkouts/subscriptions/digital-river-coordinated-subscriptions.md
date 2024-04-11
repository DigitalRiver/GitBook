---
description: >-
  If you're pairing the Direct Integration solution with Digital River's
  subscription service, learn how to handle acquisitions.
---

# Handling subscription acquisitions

If you're pairing the [Direct Integrations](../) checkout solution with [Digital River's subscription service](../../../using-our-services/subscriptions.md), this page explains how to process:

* [Standard subscription acquisitions](digital-river-coordinated-subscriptions.md#building-acquisitions)
* [Free trial subscription acquisitions](digital-river-coordinated-subscriptions.md#managing-trial-subscription-acquisitions)

Once you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you'll also need to activate the subscription, fulfill the goods, and manage renewals. For details on how to handle these, and other processes, refer to the [Managing a subscription](../../../subscription-management/managing-a-subscription.md) page.&#x20;

## Subscription acquisitions <a href="#building-acquisitions" id="building-acquisitions"></a>

During subscription acquisitions, you must:

* [Create a subscription](digital-river-coordinated-subscriptions.md#creating-a-subscription) and [handle the response](digital-river-coordinated-subscriptions.md#handling-the-response)
* [Display terms and acquire consent](digital-river-coordinated-subscriptions.md#displaying-terms-and-acquiring-consent)
* [Obtain payment information](digital-river-coordinated-subscriptions.md#acquiring-payment)

### Creating a subscription

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you define subscriptions in `items[]`. Checkouts can contain either a single `items[]` with [`subscriptionInfo`](subscription-information-1.md) or[ multiple subscription line items](digital-river-coordinated-subscriptions.md#subscriptions-with-multiple-line-items). We also support [mixed cart checkouts](digital-river-coordinated-subscriptions.md#mixed-carts).

For each `items[].subscriptionInfo` in the request:

* Use `planId` to associate the [subscription](../../../developer-resources/digital-river-api-reference/subscriptions.md) with a [plan](../../../developer-resources/digital-river-api-reference/plans.md). For details, refer to [Defining a business model](../../../using-our-services/subscriptions.md#defining-a-business-model).
* Pass `terms`. To do this, make a [`GET /plans/{planId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrievePlans) request. From the response, retrieve the [plan's](../../../developer-resources/digital-river-api-reference/plans.md) `terms` and use that value to set the line item's `terms`. If you don't send `terms`, a `400 Bad Request` with a `code` of `missing_parameter` is thrown.

{% hint style="success" %}
For details, refer to [Displaying terms and acquiring consent](digital-river-coordinated-subscriptions.md#displaying-terms-and-acquiring-consent).
{% endhint %}

* Set [`autoRenewal`](subscription-information-1.md#auto-renewal) to `true` or omit the value. If you set `autoRenewal` to `false`, you receive a `400 Bad Request` with a `code` of `invalid_parameter`.
* Use `freeTrial` to set up trial periods. For details, refer to [Trial subscription acquisitions](digital-river-coordinated-subscriptions.md#managing-trial-subscription-acquisitions).
* If you don't provide a unique `subscriptionId`, we generate one for you.

In subscription acquisitions, make sure you also set the checkout's [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `customer_initiated`.

{% tabs %}
{% tab title="POST /checkouts" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
	"customerId": "0aa4bb94-2995-4689-9b57-f11d1beb18c9",
	"sourceId": "586ffca0-ca4f-4d87-a933-192afa36cc6b",
	"locale": "en_US",
	"email": "jsmith123@digitalriver.com",
	"currency": "USD",
	"items": [{
			"skuId": "d273122b-e78d-4fcb-a1ab-10c07c871ee7",
			"quantity": 5,
			"price": 5.01,
			...
			"subscriptionInfo": {
				"planId": "460d1943-5ac1-48b8-98e8-237c6e3019a7",
				"terms": "These are the terms...."
			},
			"metadata": {
				"key1_ItemLevel": "tets"
			}
	}],
	...
}'
```
{% endtab %}
{% endtabs %}

#### Checkouts with multiple subscriptions <a href="#subscriptions-with-multiple-line-items" id="subscriptions-with-multiple-line-items"></a>

[Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) can contain multiple [`items[]`](../creating-checkouts/describing-the-items/) with [`subscriptionInfo`](subscription-information-1.md). All the recurring items however must share the same `planId` and (if you set your own value) `subscriptionId`. Once you submit the request, Digital River adds these line items to a single [subscription](../../../developer-resources/digital-river-api-reference/subscriptions.md).

If you attempt to [create checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) with multiple `items[]` that reference different plans, then the following error is returned:

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

#### Checkouts with subscription and non-subscription items <a href="#mixed-carts" id="mixed-carts"></a>

Digital River's subscription service supports building checkouts that contains both subscription and non-subscription line items and then successfully [converting those checkouts to orders](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). The subscription line items, however, must all [reference the same plan](digital-river-coordinated-subscriptions.md#subscriptions-with-multiple-line-items).

A common use case for these types of mixed checkouts is to process transactions that combine a one-time physical product with a digital subscription service.

### Handling the acquisition checkout response <a href="#handling-the-response" id="handling-the-response"></a>

After you submit the [`POST/ checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) request, Digital River creates a [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions), sets its to [`state`](../../../developer-resources/digital-river-api-reference/subscriptions.md#state) to `draft` and then generates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../../order-management/events-and-webhooks-1/events-1/#event-types) of [`subscription.created`](../../../order-management/events-and-webhooks-1/events-1/event-types.md#subscription.created).&#x20;

In the response's body and the event's `data.object`, the [`subscriptionId`](subscription-information-1.md#subscription-identifier) uniquely identifies that subscription. At a minimum, make sure you persist this value.

At this point, no additional subscription line items can be added to the checkout. Furthermore, you're restricted to [what product information can be updated](../creating-checkouts/describing-the-items/#updating-items).

Since Digital River's subscription service doesn't support manual renewals, [`autoRenewal`](subscription-information-1.md#auto-renewal) always returns `true` .

{% hint style="success" %}
For details on how to handle manual renewals, where you invite customers to actively renew subscriptions at a designated time, refer to the [Third party subscription services](third-party-coordinated-subscriptions.md) page.
{% endhint %}

{% tabs %}
{% tab title="Checkout with subscription line item" %}
```javascript
{
    "id": "88aaf811-a8a8-4b7a-9a23-5bc0241e039a",
    "createdTime": "2021-08-11T20:06:32Z",
    "customerId": "0aa4bb94-2995-4689-9b57-f11d1beb18c9",
    "currency": "USD",
    "email": "jsmith123@digitalriver.com",
    "billTo": {
        "address": {
            "line1": "10380 Bren Road West",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "Digital Development",
        "email": "testdummy@digitalriver.com",
        "organization": "DR",
        "additionalAddressInfo": {
            "neighborhood": "Centro"
        }
    },
    "totalAmount": 26.9,
    "subtotal": 25.05,
    "totalFees": 0.0,
    "totalTax": 1.85,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "id": "b0ae5bf9-6df7-4185-91f2-7e2589acbe8d",
            "skuId": "d273122b-e78d-4fcb-a1ab-10c07c871ee7",
            "amount": 25.05,
            "quantity": 5,
            "metadata": {
                "key1_ItemLevel": "tets"
            },
            "tax": {
                "rate": 0.07375,
                "amount": 1.85
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "subscriptionInfo": {
                "subscriptionId": "192a2549-8b16-482e-b1bb-b4a64cd6a0c0",
                "planId": "460d1943-5ac1-48b8-98e8-237c6e3019a7",
                "terms": "Please accept terms",
                "autoRenewal": true,
                "freeTrial": false
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            }
        }
    ],
    "updatedTime": "2021-08-11T20:06:32Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "C5_INC-ENTITY",
        "name": "DR globalTech Inc."
    },
    "liveMode": false,
    "payment": {
        "sources": [
            {
                "id": "586ffca0-ca4f-4d87-a933-192afa36cc6b",
                "type": "creditCard",
                "amount": 26.9,
                "owner": {
                    "firstName": "Digital",
                    "lastName": "Development",
                    "email": "testdummy@digitalriver.com",
                    "address": {
                        "line1": "10380 Bren Road West",
                        "city": "Minnetonka",
                        "postalCode": "55343",
                        "state": "MN",
                        "country": "US"
                    },
                    "organization": "DR",
                    "additionalAddressInfo": {
                        "neighborhood": "Centro"
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
            "id": "9fb4036f-5051-4255-9189-16e449d69ca6",
            "amountContributed": 26.9,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "9fb4036f-5051-4255-9189-16e449d69ca6_3c6275e8-e065-4bb9-b75a-829f62b78c2c"
        }
    }
}
```
{% endtab %}
{% endtabs %}

At this stage of the acquisition process, if you [retrieve the subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSubscriptions), you'll notice that key fields have yet to be populated. This is because the [subscription's](../../../developer-resources/digital-river-api-reference/subscriptions.md) `state` is still `draft` and the `contractBindingUntil`, `nextReminderDate`, `currentPeriodEndDate`, and `nextInvoiceDate` are generated when you [activate the subscription](../../../subscription-management/managing-a-subscription.md#activating-a-subscription).

{% tabs %}
{% tab title="Subscription prior to activation" %}
```javascript
{
    "id": "7f784dd8-a76f-4d3a-84e1-abdc9c7ac3b9",
    "createdTime": "2022-02-07T14:02:46Z",
    "updatedTime": "2022-02-07T14:02:46Z",
    "stateTransitions": {},
    "taxInclusive": false,
    "currency": "USD",
    "planId": "82cbf763-fa27-401a-aa69-5e6640539ce7",
    "state": "draft",
    "items": [
        {
            "price": 100.0,
            "skuId": "bd933514-43fa-40d3-863c-8ff6fce0db76",
            "quantity": 1
        }
    ],
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

### Displaying terms and acquiring consent

During acquisitions, you must disclose a subscription's terms and then acquire the customer's active acceptance of them. How you do this depends on whether you're using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md). In either case, the [plan's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Plans) [`terms`](../../../developer-resources/digital-river-api-reference/plans.md#terms) should match those displayed to customers.

{% hint style="info" %}
For details on required disclosures, see the [Subscriptions and Auto-Renewal Considerations](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=23d0d88adb5c341046e8d6aa489619ae) article (_refer to_ [_Learning tools_](../../../general-resources/standards-and-certifications/compliance-requirements.md#accessing-the-learning-tools) _for access information_).
{% endhint %}

{% tabs %}
{% tab title="Drop-in payments" %}
If you're using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/), a subscription's terms are displayed in the modal window. For details, see the [Acquiring payment section](digital-river-coordinated-subscriptions.md#acquiring-payment) on this page.
{% endtab %}

{% tab title="Elements" %}
If you're using [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md), present our standardized subscription terms and save payment agreement by calling the [get compliance details method](../../../developer-resources/reference/digitalriver-object.md#digitalriver.compliance.getdetails-businessentitycode-locale), retrieving `autorenewalPlanTerms.localizedText` and then displaying that text with an appropriate acceptance control.

![](<../../../.gitbook/assets/DR js terms.png>)

Your code should be written so that customers must accept these terms before the checkout can proceed. You can then use `autorenewalPlanTerms.localizedText` to set `mandate.terms` in the [`createSource()`](digital-river-coordinated-subscriptions.md#creating-a-new-payment-source) method's configuration object. &#x20;
{% endtab %}
{% endtabs %}

After you [convert an acquisition checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the subscription's terms are stored in the [billing agreement](subscription-information-1.md#billing-agreements).

### Acquiring payment

During acquisition checkouts, you can give customers the option to:

* [Create a new payment source](digital-river-coordinated-subscriptions.md#creating-a-new-payment-source) or
* [Authenticate a saved payment source](digital-river-coordinated-subscriptions.md#authenticating-a-saved-payment-source)

#### Creating a new payment source

How you create a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) to fund a recurring transaction depends on whether your integration uses [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).

{% hint style="success" %}
For more details, refer to the [subscriptions section](../building-you-workflows/#subscription) on the [Building payment workflows](../building-you-workflows/) page.
{% endhint %}

{% tabs %}
{% tab title="Drop-in payments" %}
After [building a checkout with subscription information](digital-river-coordinated-subscriptions.md#creating-a-subscription), configure [`createDropin()`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate):

* Use the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier) to set `sessionId`
* If your integration sends the customer's billing information in the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `billTo`, then it's not necessary to pass `billingAddress`
* In [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options-1), set:
  * [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout`
  * [`showComplianceSection`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-compliance-section) to `true`
  * [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `subscription`
  * [`showTermsOfSaleDisclosure`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-terms-of-sale-disclosure) to `true` and [`showSavePaymentAgreement`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-save-payment-agreement) to `false`. These two settings (along with the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`autoRenewal`](subscription-information-1.md#auto-renewal) value of `true`) prompt Drop-in payments to display the combined autorenewal and save payment agreement.

```javascript
let digitalriverpayments = new DigitalRiver("pk_hc_a209389e4588433bb6e00b32466b82c3", {
    "locale": "en_US"
});

let configuration = { 
    "sessionId": "2bc96772-1142-4289-9d20-f6905591d7e4",
    "options": {
        "flow": "checkout",
        "showComplianceSection": true,
        "showSavePaymentAgreement": false,
        "showTermsOfSaleDisclosure": true,
        "usage": "subscription"
    }
    ...
}

let dropin = digitalriverpayments.createDropin(configuration);
dropin.mount("drop-in-container");
```

Pass the configuration object to `createDropin()`and [mount Drop-in payments](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-7-mount-drop-in-payments-on-a-checkout-or-account-management-page) in the appropriate container. If the request is successful, [`onReady`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-events) returns the transaction's eligible payment methods:

```javascript
{
    "paymentMethodTypes": [
        "creditCard",
        "payPalBilling",
        "googlePay",
        "klarnaCreditRecurring",
        "msts"
    ]
}
```

Each payment method, accompanied by the subscription's terms and conditions, is displayed in the modal window.

If customers click the [configurable continue button](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) without agreeing to the terms, Drop-in prevents the transaction from proceeding.

![](<../../../.gitbook/assets/image (74).png>)

If customers consent to the terms and submit their payment information and the resulting create source request is successful, then the [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-events) event's `data` contains a [`source`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) and [`chargeable`](../../../payments/payment-sources/#source-state). The object also contains the agreed-upon terms (`mandate.terms`) and the time the customer accepted those terms (`mandate.signedTime`).

For details, refer to the [Drop-in payments integration guide](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md) and the [Drop-in payments builder tool](https://drapi.io/drop-in-builder/).
{% endtab %}

{% tab title="Elements" %}
After [building a checkout with subscription information](digital-river-coordinated-subscriptions.md#creating-a-subscription), send the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier) to your front end and use it to set `sessionId` in the configuration object of [`retrieveAvailablePaymentMethods()`](../../../developer-resources/reference/digitalriver-object.md#digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters).

```javascript
...
digitalRiver.retrieveAvailablePaymentMethods({
    "sessionId": "1c86a97f-45ea-4d73-8c99-ca533e392ab1"
}).then(function(result) {
    //do something with the result
    console.log(result)
});
...
```

If the request is successful, the response contains the payment methods that are applicable to the transaction.

{% code title="Available payment methods" %}
```javascript
[
    {
        "type": "creditCard",
        "flow": "standard",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/creditcard.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "Credit Card",
        "localizedDisplayName": "Credit Card"
    },
    {
        "type": "payPalBilling",
        "flow": "redirect",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/paypalBilling.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "PayPal Billing",
        "localizedDisplayName": "PayPal"
    },
    {
        "type": "googlePay",
        "flow": "standard",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/googlepay.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "Google Pay",
        "localizedDisplayName": "Google Pay"
    }
]
```
{% endcode %}

Based on these payment methods, [create the appropriate elements](../../../developer-resources/reference/digitalriver-object.md#creating-elements) to collect the customer's sensitive payment information.

After customers select a payment method, [accept the terms](digital-river-coordinated-subscriptions.md#displaying-terms-and-acquiring-consent) and submit their payment information, configure [`createSource()`](../../../developer-resources/reference/digitalriver-object.md#creating-sources):

* Set `type` to the payment method selected by the customer
* Use the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier) to set `sessionId`.
* Set [`usage`](../../../developer-resources/reference/digitalriver-object.md#specifying-a-sources-future-use) to `subscription` and `futureUse` to `true`
* Use the [agreed upon terms](digital-river-coordinated-subscriptions.md#displaying-terms-and-acquiring-consent) to set `mandate.terms`
* If your integration passes a customer's billing information in the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `billTo`, then it's not necessary to send `billingAddress`

```javascript
var payload = {
    "type": "creditCard",
    "sessionId": "1c86a97f-45ea-4d73-8c99-ca533e392ab1",
    "futureUse": true,
    "usage": "subscription",
    ...
    "mandate": {
        "terms": "By checking the box below and completing your purchase..."
    }
}

digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```

If the create source request is successful, the response contains a [`source`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) and [`chargeable`](../../../payments/payment-sources/#source-state).

For more information, refer to the [Elements integration guide](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).
{% endtab %}
{% endtabs %}

Next, send the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) identifier and [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) to your back-end.

Submit a [`POST /customers/{customerId}/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCustomerSource) to attach the source to the customer. This flips the source's [`reusable`](../../../payments/payment-sources/#reusable-or-single-use) attribute to `true`, meaning the object can be used in both the subscription's acquisition and as the designated source in renewals.

Once saved to the customer, your integration should then [attach the source to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

You should also retrieve `mandate.terms` from the source and use this value to set each of the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`items[].subscriptionInfo.terms`](subscription-information-1.md#terms). This ensures that the subscription's terms are added to the [billing agreement](subscription-information-1.md#billing-agreements).

#### Authenticating a saved payment source

{% hint style="warning" %}
[Drop-in payments](../../../payments/payment-integrations-1/drop-in/) does not currently support retrieving saved payment methods.
{% endhint %}

If you give customers the option to select a saved payment source during subscription acquisitions, then after [building a checkout with subscription information](digital-river-coordinated-subscriptions.md#creating-a-subscription), send the [payment session identifier](../creating-checkouts/#payment-session-identifier) to your front end and use it to set `sessionId` in the configuration object of [`retrieveAvailablePaymentMethods()`](../../../developer-resources/reference/digitalriver-object.md#digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters).

{% tabs %}
{% tab title="Request" %}
```javascript
...
digitalRiver.retrieveAvailablePaymentMethods({
    "sessionId": "1c86a97f-45ea-4d73-8c99-ca533e392ab1"
}).then(function(result) {
    //do something with the result
    console.log(result)
});
...
```
{% endtab %}

{% tab title="Response" %}
{% code title="Available payment methods" %}
```javascript
[
    {
        "type": "creditCard",
        "flow": "standard",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/creditcard.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "Credit Card",
        "localizedDisplayName": "Credit Card"
    },
    {
        "type": "payPalBilling",
        "flow": "redirect",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/paypalBilling.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "PayPal Billing",
        "localizedDisplayName": "PayPal"
    },
    {
        "type": "googlePay",
        "flow": "standard",
        "supportsRecurring": true,
        "supportsFreeTrial": true,
        "images": {
            "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/googlepay.png"
        },
        "supportsStorage": true,
        "defaultMandate": {
            "terms": "I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur at a future date."
        },
        "displayName": "Google Pay",
        "localizedDisplayName": "Google Pay"
    }
]
```
{% endcode %}
{% endtab %}
{% endtabs %}

For each payment method contained in the response, determine if its `type` matches the `type` of one or more of the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `sources[]`. If it does, you can retrieve those saved `sources[]` from the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and display them as options on your payments page.

If the customer selects a saved source, pass its `sources[].id` and `sources[].clientSecret` (along with the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier)) to [`authenticateSource()`](../../../developer-resources/reference/digitalriver-object.md#authenticating-sources). This method determines whether [strong customer authentication](../../../payments/psd2-and-sca/) is required.

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "533319260336",
    ...
    "sources": [
        {
            "id": "5e359d60-1d23-4234-84ee-e1c9b3ed7edc",
            ...
            "type": "creditCard",
            "reusable": true,
            "state": "chargeable",
            ...
            "clientSecret": "5e359d60-1d23-4234-84ee-e1c9b3ed7edc_bf74c04c-8586-41e2-964a-f5e618d2b7e3",
            ...
        },
        {
            "id": "19f47eba-418f-41b3-882c-462e335770e7",
            ...
            "type": "payPalBilling",
            "reusable": true,
            "state": "chargeable",
            ...
            "clientSecret": "19f47eba-418f-41b3-882c-462e335770e7_cc871d23-474d-4a3f-9803-4e98fa39f2ee",
            ...
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="Checkout" %}
```javascript
{
    "id": "50a72152-4a61-4e4a-b9e1-2ab5db891105",
    ...
    "payment": {
        "session": {
            "id": "f5dd814a-ecee-4f7e-bf7c-4635f0c19c91",
            ...
        }
    }
}
```
{% endtab %}

{% tab title="authenticateSource( )" %}
```javascript
...
digitalriver.authenticateSource({
    "sessionId": "f5dd814a-ecee-4f7e-bf7c-4635f0c19c91",
    "sourceId": "5e359d60-1d23-4234-84ee-e1c9b3ed7edc",
    "sourceClientSecret": "5e359d60-1d23-4234-84ee-e1c9b3ed7edc_bf74c04c-8586-41e2-964a-f5e618d2b7e3",
    "returnUrl": "https://mypage.com"
});
...
```
{% endtab %}
{% endtabs %}

If the response `status` is `complete` or `authentication_not_required`, the method resolves, allowing your integration to [attach the authenticated source to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% hint style="success" %}
For additional details, refer to the section on [retrieving saved payment sources during subscription acquisitions](../building-you-workflows/#customer-saves-credit-card-details-during-subscription-acquisition-checkout) on the [Building payment workflows](../building-you-workflows/) page.
{% endhint %}

### Managing subscriptions after acquisition

After you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you'll need to active the subscription and process renewals. To learn more, refer to the [Managing a subscription](../../../subscription-management/managing-a-subscription.md) page.

## Trial subscription acquisitions <a href="#managing-trial-subscription-acquisitions" id="managing-trial-subscription-acquisitions"></a>

You handle free-trial subscription acquisitions in much the same way as [standard acquisitions](digital-river-coordinated-subscriptions.md#building-acquisitions).

In [free trials](../../../using-our-services/subscriptions.md#setting-up-free-trials), however, you must configure the checkout in a slightly different way.&#x20;

Once customers initiate checkout, determine whether their cart contains any trial-based subscription products. If it does, use `items[].subscriptionInfo` to describe those products in your [`POST /checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

{% hint style="info" %}
You can also add non-trial subscription products, as well as non-subscription products, to the same checkout. All the subscription line items, however, must reference the same [plan](../../../developer-resources/digital-river-api-reference/plans.md). For details, refer to [Checkouts with multiple subscriptions](digital-river-coordinated-subscriptions.md#subscriptions-with-multiple-line-items).
{% endhint %}

Each trial-based subscription line item in the request must specify a `price` of `0.0`, set `freeTrial` to `true`, and pass a `planId` that references a [trial period plan](../../../using-our-services/subscriptions.md#trial-period-plans).

{% code title="POST /checkouts" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "customerId": "563089630336",
    "sourceId": "8687447b-a04d-4838-af6c-0de0810f23a7",
    "locale": "en_US",
    "email": "jdoe@digitalriver.com",
    "currency": "USD",
    "items": [
        {
            "skuId": "sku_3e5ab173-d52e-4d9e-8888-2a00f6bb188e",
            "quantity": 2,
            "price": 0.0,
            "subscriptionInfo": {
                "planId": "186cf07e-a1ea-4ec0-9d9a-8aa93b3af43a",
                "terms": "The terms of the subscription",
                "autoRenewal": true,
                "freeTrial": true
            }
        }       
    ]
}'
```
{% endcode %}

If you create or update a checkout and (1) `freeTrial` is `true` and `price` or `aggregatePrice` contain a value that's greater than `0.0` or (2) `freeTrial` is `false` and `price` or `aggregatePrice` are `0.0`, then the following error is thrown:

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

### Managing trial subscriptions after acquisition

For details on how to process a trial subscription after you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), refer to [Trial subscription management](../../../subscription-management/managing-a-subscription.md#trial-subscription-management) on the [Managing a subscription](../../../subscription-management/managing-a-subscription.md) page.
