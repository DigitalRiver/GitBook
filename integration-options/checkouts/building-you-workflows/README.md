---
description: >-
  Learn how to create SCA-compliant workflows using Drop-in payments or
  Elements.
---

# Building payment workflows

Using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [Elements](../../../payments/payment-integrations-1/digitalriver.js/), you can create [Strong Customer Authentication (SCA)](../../../payments/psd2-and-sca/) compliant workflows for both [purchase transactions](./#purchase-flows) and [account management](./#account-management-flows).

Whichever payment solution you're using, all SCA requirements are managed by Digital River. Two-factor authentication is handled by our [authenticate source method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources). And our card acquirers use the [3-D Secure](https://en.wikipedia.org/wiki/3-D\_Secure) protocol to communicate with issuing banks. This protocol operates "behind-the-scenes" and requires no developer interaction.

## Key settings and methods <a href="#key-settings-and-methods" id="key-settings-and-methods"></a>

The following chart lists some of the key settings and methods you should use when building purchase and account management flows. It's meant to be read from left-to-right and top-to-bottom. For example:

* In [one-off purchase flows](./#one-off) in which customers [save a new payment source to their account](./#credit-card-details-saved-by-customer-during-checkout), you should set the checkout's [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `customer_initiated`. If you're using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/), use the [`createDropIn()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in) method's [configurable `options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options-1) to set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout` and [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `convenience`. With [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md), use the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object to set `futureUse` to `true` and [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) to `convenience`.
* When customers are [acquiring an auto-renewing subscription](./#subscription), and decide to [retrieve a payment source saved to their account](./#customer-saves-credit-card-details-during-subscription-acquisition-checkout), set the checkout's `chargeType` to `customer_initiated` and [`autoRenewal`](../subscriptions/subscription-information-1.md#auto-renewal) to `true`. In this flow type, [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) is not supported. Instead, you'll need to use the [`authenticateSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources) method.

![Click to enlarge image](<../../../.gitbook/assets/flow configurations.png>)

## Common Drop-in payments steps <a href="#common-drop-in-steps" id="common-drop-in-steps"></a>

For any workflow that uses [Drop-in payments](../../../payments/payment-integrations-1/drop-in/), whether it's intended to handle [purchases](./#purchase-flows) or [account management](./#account-management-flows), you first need to perform the following steps:

1. ​[Include DigitalRiver.js on your page](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-1-include-digitalriver-js-on-your-page).
2. ​[Include the Drop-in CSS file](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-2-include-the-hydrate-css-file).
3. ​[Initialize DigitalRiver.js with your public key](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-3-initialize-digitalriver-js-with-your-public-key).
4. ​[Create a container for Drop-in payments](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#step-4-create-a-container-for-drop-in).

## Elements prerequisites

If you're using [Elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md) to build [purchase](./#purchase-flows) workflows, make sure you [complete the necessary migration to payment sessions](../creating-checkouts/payment-sessions.md#migrating-to-payment-sessions). We also assume you are familiar with [creating and styling elements](../../../developer-resources/reference/elements/) as well as the [basics of capturing payment details](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).

## Purchase flows <a href="#purchase-flows" id="purchase-flows"></a>

For almost all [one-off](./#one-off), [subscription](./#subscription), and [mail-order/telephone-order (MOTO)](./#mail-order-telephone-order) transactions, Digital River supports [SCA-compliant](../../../payments/psd2-and-sca/) workflows that use either [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) or [Elements](../../../payments/payment-integrations-1/digitalriver.js/quick-start.md).‌

### One-off <a href="#one-off" id="one-off"></a>

‌One-off workflows allow customers to [enter](./#credit-card-details-entered-by-customer-during-checkout), [save](./#credit-card-details-saved-by-customer-during-checkout), and [retrieve](./#customer-selects-saved-credit-card-during-checkout) their payment information while making one-time purchases.

#### Customers enter their payment information <a href="#credit-card-details-entered-by-customer-during-checkout" id="credit-card-details-entered-by-customer-during-checkout"></a>

‌In this [one-off](./#one-off) flow, customers supply their payment information, but don't save it to their account.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

{% tabs %}
{% tab title="Drop-in payments " %}
**Prerequisites**: Perform the [common Drop-in payments steps](./#common-drop-in-steps).

**Step one**: [Build a checkout](../creating-checkouts/) with all tax, shipping, duty and fee amounts in a final state and a [`chargeType`](../creating-checkouts/initiating-a-charge.md) that is `customer_initiated`.

**Step two**: Retrieve the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier), and use it to set [`sessionId`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) in the[ configuration object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments). In `options`, set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout` and [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `convenience`.

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        flow: "checkout",
        usage: "convenience"
    }
    ...
}
```

**Step three**: Pass the configuration object to the [create Drop-in method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in).

```javascript
let dropin = digitalriver.createDropin(configuration);
```

**Step four**: On your checkout page, Drop-in payments renders in the designated container.

![](<../../../.gitbook/assets/rendered drop-in.PNG>)

Customers enter their payment information and click the [configurable](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) pay now button.

If customers complete any [SCA](../../../payments/psd2-and-sca/) that may be required, [`onSuccess` ](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess)returns a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step six**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section.

**Step one:** [Build a checkout](../creating-checkouts/) with all tax, shipping, duty and fee amounts in a final state and a [`chargeType`](../creating-checkouts/initiating-a-charge.md) that is `customer_initiated`.

**Step two:** Retrieve the [payment session identifier ](../creating-checkouts/#payment-session-identifier)and assign it to `sessionId` in the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object. You should also set `futureUse` to `false` and [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) to `convenience`.

```javascript
let payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "futureUse": false,
    "usage": "convenience",
    ...
}

digitalriver.createSource(payload).then(function(result) {
    if(result.state === "chargeable") {
        sendToBackEnd(result);
    } else {
        doErrorScenario();
    }
});
```

After the method is called and customers complete any SCA that may be required, a unique [source](../../../payments/payment-sources/) is returned.

**Step three:** [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step four**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}

#### Customers save their payment information <a href="#credit-card-details-saved-by-customer-during-checkout" id="credit-card-details-saved-by-customer-during-checkout"></a>

In this [one-off](./#one-off) flow, customers enter payment information and save it to their account.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
**Prerequisites**: Perform the [common Drop-in payments steps](./#common-drop-in-steps).

**Step one**: [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. The [`chargeType`](../creating-checkouts/initiating-a-charge.md) should be `customer_initiated`.

**Step two**: Retrieve the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier) and use it to set [`sessionId`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) in the [Drop-in payments' configuration object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments). You should also use `options` to set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout`, [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `convenience`, and [`showSavePaymentAgreement`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-save-payment-agreement) to `true`.

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        "flow": "checkout",
        "showSavePaymentAgreement": true,
        "usage": "convenience"
    },
    ...
}
```

**Step three**: Pass the configuration object to the [create Drop-in method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in).

```javascript
let dropin = digitalriver.createDropIn(configuration);
```

**Step four**: On your checkout page, Drop-in payments renders in the designated container.

![](<../../../.gitbook/assets/rendered drop-in with saved payment method option.PNG>)

Customers enter their credit card information, actively accept the save payment agreement and click the [configurable](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) pay now button.

If customers complete any [SCA](../../../payments/psd2-and-sca/) that may be required, [`onSuccess` ](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess)returns a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five**: [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

**Step six**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step seven**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section. Your flow also needs to display the storage terms and provide customers the option of saving their payment information.

**Step one:** [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. The [`chargeType`](../creating-checkouts/initiating-a-charge.md) should be `customer_initiated`.

**Step two:** Retrieve the [payment session identifier ](../creating-checkouts/#payment-session-identifier)and assign it to `sessionId` in the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object.  You should also set `futureUse` to `true` and [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) to `convenience`. Use `mandate.terms` to pass the save payment agreement that the customer accepts.

```javascript
var payload = {
    "type": "creditCard",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "futureUse": true,
    "usage": "convenience",
    ...
    "mandate": {
        "terms": "Yes, please save this account and payment information for future purchases."
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

After the method is called and customers complete any SCA that may be required, a unique [source](../../../payments/payment-sources/) is returned.

**Step three:** [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

**Step four**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step five**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}

#### Customers retrieve their payment information <a href="#customer-selects-saved-credit-card-during-checkout" id="customer-selects-saved-credit-card-during-checkout"></a>

In this one-off purchase flow, customers select a payment method that they previously saved to their account. The key step is to call the [authenticate source method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources).

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | No                          | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
[Drop-in payments](../../../payments/payment-integrations-1/drop-in/) does not currently support retrieving saved payment methods. In order to handle this flow, use [Elements](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section.

**Step one:** [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. The [`chargeType`](../creating-checkouts/initiating-a-charge.md) should be `customer_initiated`.

**Step two:** [Retrieve the customer's payment sources](../../../payments/payment-sources/retrieving-sources.md#obtain-a-customers-sources) and display them during the checkout process.

**Step three**: If the customer opts to use a saved payment method, you'll need to determine whether SCA is required. To do this, configure and call the [`authenticateSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources) method.

```javascript
...
digitalriver.authenticateSource({
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
}).then(function(data) {

});
...
```

After the method is invoked, Digital River handles any required SCA. Once authentication is complete or is determined not to be necessary, the method resolves, allowing the checkout flow to continue.

If authentication is successful, Digital River returns the [source](../../../payments/payment-sources/) in a [`chargeable` state](../../../payments/payment-sources/#source-state).

**Step four**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-a-source-to-a-customer).

**Step five:** [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}

### Subscription <a href="#subscription" id="subscription"></a>

You can create [SCA-compliant](../../../payments/psd2-and-sca/) workflows that allow customers to either [save](./#customer-enters-credit-card-details-during-subscription-acquisition-checkout) or [retrieve](./#customer-saves-credit-card-details-during-subscription-acquisition-checkout) a [recurring payment method](../../../payments/supported-payment-methods/) during subscription acquisitions. You can also set up workflows for [merchant-initiated autorenewals](./#merchant-initiated-auto-renewals).&#x20;

{% hint style="warning" %}
SCA is required for [subscription acquisitions](../subscriptions/subscription-information-1.md#subscription-acquisition) but not [merchant-initiated](../creating-checkouts/initiating-a-charge.md#merchant-initiated) auto-renewals.
{% endhint %}

#### Customers enter and save their payment information during a subscription acquisition <a href="#customer-enters-credit-card-details-during-subscription-acquisition-checkout" id="customer-enters-credit-card-details-during-subscription-acquisition-checkout"></a>

In this flow, customers save payment information to their account and use that payment source to acquire an auto-renewing subscription.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
**Prerequisites**: Perform the [common drop-in steps](./#common-drop-in-steps).

**Step one**: [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. Set [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `customer_initiated` and `autoRenewal` to `true`.

**Step two**: Retrieve the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier), and use it to set [`sessionId`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) in the [configuration object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments). In [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options-1), set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout`, [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `subscription`, and [`showTermsOfSaleDisclosure`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-terms-of-sale-disclosure) to `true`.

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        "flow": "checkout",
        "showTermsOfSaleDisclosure": true,
        "usage": "subscription"
    },    
    ...
}
```

**Step three**: Pass the configuration object to the [create Drop-in method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in).

```javascript
let dropin = digitalriver.createDropIn(configuration);
```

**Step four**: On your checkout page, Drop-in payments renders in the designated container.

![](<../../../.gitbook/assets/sub terms.png>)

Customers must enter their payment information, actively accept the terms and click the [configurable](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) pay now button.

If customers complete any [SCA](../../../payments/psd2-and-sca/) that may be required, [`onSuccess` ](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess)returns a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five:** [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

**Step six**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step seven**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section. At some point during the flow, you also need to display the subscription's terms and save payment agreement and acquire the customer's active acceptance of them.

**Step one**: [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. Set [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `customer_initiated` and `autoRenewal` to `true`.

**Step two:** Once the customer selects the option to save the payment method and agrees to the displayed terms, retrieve the [payment session identifier ](../creating-checkouts/#payment-session-identifier)and assign it to `sessionId` in the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object. You should also set `futureUse` to `true` and [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) to `subscription`. Use `mandate.terms` to pass the save payment agreement that the customer accepts.

```javascript
var payload = {
    "type": "creditCard",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "futureUse": true,
    "usage": "subscription",
    ...
    "mandate": {
        "terms": "Yes, please save this account and payment information for future purchases."
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

After the method is called and customers complete any SCA that may be required, a unique [source](../../../payments/payment-sources/) is returned.

**Step three:** [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

**Step four:** [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step five:** [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}

#### Customers retrieve saved payment during a subscription acquisition <a href="#customer-saves-credit-card-details-during-subscription-acquisition-checkout" id="customer-saves-credit-card-details-during-subscription-acquisition-checkout"></a>

In this flow, customers select a credit card they previously saved to their account and use it to acquire an auto-renewing subscription.

‌The key step is to call the [authenticate source method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources).

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | No                          | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
[Drop-in payments](../../../payments/payment-integrations-1/drop-in/) does not currently support retrieving stored payment methods. In order to handle this flow, use Elements.
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section.

**Step one**: [Build a checkout](../creating-checkouts/) with a [registered customer](../creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and all tax, shipping, duty and fee amounts in a final state. Set [`chargeType`](../creating-checkouts/initiating-a-charge.md) to `customer_initiated` and `autoRenewal` to `true`.

**Step two:** [Retrieve the customer's payment sources](../../../payments/payment-sources/retrieving-sources.md#obtain-a-customers-sources) and display them to the customer during the checkout process.

**Step three**: If the customer opts to use a saved payment method, configure and call the [`authenticateSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources) method.

```javascript
...
digitalriver.authenticateSource({
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
}).then(function(data) {

});
...
```

After invoking this method, Digital River automatically handles any required SCA. Once authentication is complete or is determined not to be necessary, the method resolves, allowing the checkout flow to continue, and returns a unique [Source](../../../payments/payment-sources/).

**Step four**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step five:** [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}

#### Merchant-initiated auto renewals <a href="#merchant-initiated-auto-renewals" id="merchant-initiated-auto-renewals"></a>

In this workflow, a merchant initiates the auto-renewal of a subscription. Although this type of workflow doesn't require SCA, you should ensure you're correctly handling auto-renewing subscriptions.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | N/A                         | N/A                 |

### Mail order/telephone order <a href="#mail-order-telephone-order" id="mail-order-telephone-order"></a>

[SCA](../../../payments/psd2-and-sca/) is not required for transactions where customers provide their payment details by regular mail, fax, or telephone. But both Drop-in payments and Elements support building workflows for [mail order and telephone order](../creating-checkouts/initiating-a-charge.md#mail-order-telephone-order) (MOTO) transactions.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | Yes                         | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
**Prerequisites**: Perform the [common Drop-in payments steps](./#common-drop-in-steps).

**Step one**: [Build a checkout](../creating-checkouts/) with a [`chargeType`](../creating-checkouts/initiating-a-charge.md) of [`moto`](../creating-checkouts/initiating-a-charge.md#merchant-initiated) and all tax, shipping, duty and fee amounts in a final state. This configures Drop-in payments to display only payment methods that are supported in MOTO transactions.

**Step two**: Retrieve the checkout's [payment session identifier](../creating-checkouts/#payment-session-identifier), and use it to set [`sessionId`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) in the [Drop-in payments' configuration object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments). In `options`, set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `checkout` and [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) to `convenience`.

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        flow: "checkout",
        usage: "convenience"
    }
    ...
}
```

**Step three**: Pass the configuration object to the [create Drop-in method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in).

```javascript
let dropin = digitalriver.createDropin(configuration);
```

**Step four**: On your checkout page, Drop-in payments renders in the designated container.

![](../../../.gitbook/assets/MOTO.png)

The merchant's representative enters the customer's credit card information and clicks the [configurable](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) pay now button. If the payment is authorized, then [`onSuccess` ](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess)returns a unique [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) in a [`chargeable` state](../../../payments/payment-sources/#source-state).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five**: [Attach the Source to the Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step six**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section.

**Step one**: [Build a checkout](../creating-checkouts/) with a [charge type](../creating-checkouts/initiating-a-charge.md) of `moto` and all tax, shipping, duty and fee amounts in a final state.

**Step two:** Retrieve the [payment session identifier ](../creating-checkouts/#payment-session-identifier)and assign it to `sessionId` in the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object. You should also set `futureUse` to `false` and [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) to `convenience`.

```javascript
let payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "futureUse": false,
    "usage": "convenience",
    ...
}

digitalriver.createSource(payload).then(function(result) {
    if(result.state === "chargeable") {
        sendToBackEnd(result);
    } else {
        doErrorScenario();
    }
});
```

After the method is called and customers complete any SCA that may be required, a unique [source](../../../payments/payment-sources/) is returned.

**Step three:** [Attach the Source to a Checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

**Step four**: [Convert the Checkout to an Order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).
{% endtab %}
{% endtabs %}



## Account management flows <a href="#account-management-flows" id="account-management-flows"></a>

You can create flows that allow customers to manage [recurring payment methods](../../../payments/supported-payment-methods/) through their account portal.&#x20;

In these account management flows, you only need to adhere to [SCA regulations](../../../payments/psd2-and-sca/) when [saving a customer's credit card for future use](./#saving-a-credit-card-for-future-use). While storing a card, attempt to identify the intended use of the source. This increases the probability that future transactions will be approved.

You're not required to do SCA when [updating a credit card's expiration date or billing address](./#updating-a-credit-cards-expiration-date-or-billing-address).

### Saving a credit card for future use <a href="#saving-a-credit-card-for-future-use" id="saving-a-credit-card-for-future-use"></a>

In this flow, customers use their account portal to save payment information for use in future transactions.&#x20;

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
**Prerequisites**: Perform the [common drop-in steps](./#common-drop-in-steps).

**Step one**: On the page where customers manage their payment methods, use the [configuration object's](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments) [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options-1) to set [`flow`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#flow) to `managePaymentMethods` and specify a value for [`usage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use) that identifies the likely future use of the payment.

If customers are replacing an active subscription's recurring billing instrument, make sure you set `usage` to `subscription` and [`showTermsofSaleDisclosure`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#show-save-payment-agreement) to `true`. This prompts Drop-in payments to display a recurring billing agreement and forces customers to accept it.

Because this is a `managePaymentMethods` flow, and there's no [payment session](../creating-checkouts/payment-sessions.md) to reference, you shouldn't provide a [`sessionId`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options). As a result, you'll need to pass the billing information you collect from customers in [`billingAddress`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#billing-address).\


**Step three**: Pass the configuration object to the [create Drop-in method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in).

```javascript
let dropin = digitalriver.createDropIn(configuration);
```

**Step four**: On your checkout page, Drop-in payments renders in the designated container.

![](<../../../.gitbook/assets/Account Management Flow.PNG>)

Customers enter their payment information, select the save payment agreement option and click the [configurable](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-button) add payment method button.

If customers complete any [SCA](../../../payments/psd2-and-sca/) that may be required, [`onSuccess` ](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess)returns a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five**: [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section. You also need to display the save payment agreement and acquire the customer's active acceptance.

**Step one**: Once a customer selects the option to save a payment method and agrees to the displayed terms, use the [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources) method's configuration object to set `futureUse` to `true`.&#x20;

Make sure you also assign a value to [`usage`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#specifying-a-sources-future-use) that identifies the future use of the payment source and pass the `mandate.terms` that the customer agreed to on your storefront.

```javascript
var payload = {
    "type": "creditCard",
    "futureUse": true,
    "usage": "subscription",
    ...
    "mandate": {
        "terms": "Yes, please save this account and payment information for future purchases."
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

Once the customer provides the required SCA, a Source in a [`chargeable` state](../../../payments/payment-sources/#source-state) is returned.

**Step two:** [Attach the Source to the Customer](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).
{% endtab %}
{% endtabs %}

### Updating a credit card's expiration date or billing address

In this flow, customers use their account portal to update the expiration date or billing address on a saved credit card.

| SCA required? | Drop-in payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | No                          | Yes                 |

{% tabs %}
{% tab title="Drop-in payments" %}
[Drop-in payments](../../../payments/payment-integrations-1/drop-in/) does not support interacting directly with saved payment methods‌
{% endtab %}

{% tab title="Elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](./#elements-prerequisites) section.

**Step one:** [Retrieve the customer's payment sources](../../../payments/payment-sources/retrieving-sources.md#obtain-a-customers-sources) and display them to the customer.

The customer selects the payment method to update.

**Step two:** Capture the updated expiration date or billing address from the customer and pass it to the [update source method](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#updating-sources).
{% endtab %}
{% endtabs %}
