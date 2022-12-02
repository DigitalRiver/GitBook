---
description: >-
  Learn how to create SCA-compliant workflows using Drop-in Payments and
  DigitalRiver.js with elements.
---

# Building payment workflows

You can create [Strong Customer Authentication (SCA)](https://info.digitalriver.com/rs/348-QUY-258/images/Digital\_River\_Guide\_to\_PSD2\_Compliance\_2020.pdf) compliant workflows for both [purchase transactions](building-your-workflows.md#purchase-flows) and [customer account management](building-your-workflows.md#account-management-flows).

For all the workflows that use [Drop-in Payments](payments-solutions/drop-in/), you'll first need to perform some [common, initial steps](building-your-workflows.md#common-drop-in-steps) before proceeding to the workflow's specific steps.‌ For workflows using [DigitalRiver.js with elements](payments-solutions/digitalriver.js/), to complete some [prerequisites](building-your-workflows.md#elements-prerequisites).

Each purchase and account management workflow has some [key settings and methods](building-your-workflows.md#common-drop-in-steps).&#x20;

Whether you are using [Drop-in Payments](payments-solutions/drop-in/) or [DigitalRiver.js with elements](payments-solutions/digitalriver.js/), any SCA requirements are automatically managed by Digital River. Two-factor authentication is handled by our [authenticate source method](broken-reference). And our card acquirers use the [3-D Secure](https://en.wikipedia.org/wiki/3-D\_Secure) protocol to communicate with issuing banks. This protocol operates "behind-the-scenes" and requires no developer interaction.&#x20;

## Limitations and constraints

Note the following limitations and constraints when building your payments workflow.

* Do not change the currency when there is a secondary source in the cart. Specify the correct currency when creating a [secondary payment source](sources/using-the-source-identifier.md#secondary-payment-sources). After you [apply the secondary source](sources/using-the-source-identifier.md#creating-secondary-sources) to the cart, do not change the currency.\
  \
  If you change the currency when calling /v1/shoppers, a [`409 Conflict`](../error-codes.md#409-conflict) response contains specific information about what triggered the failure. In this instance, one of the currencies in the cart is not supported.

{% code overflow="wrap" %}
```json
{
    "errors": {
        "error": [
            {
                "relation": "https://developers.digitalriver.com/v1/shoppers/ShoppersResource",
                "code": "invalid-request",
                "description": "One or more sources in the cart does not support locale {Locale} and currency {Currency}."
            }
        ]
    }

}
```
{% endcode %}

* At this time, you cannot use store credit to purchase a subscription product.
* At this time, you cannot use store credit to pre-order a product.
* At this time, you cannot use store credit to purchase a product on backorder.
* At this time, you cannot attach more than one store credit source to an order. Multiple secondary sources are not supported.

## Common Drop-in Payment steps <a href="#common-drop-in-steps" id="common-drop-in-steps"></a>

For any workflow that uses [Drop-in Payments](payments-solutions/drop-in/), whether it's a [purchase](building-your-workflows.md#purchase-flows) or [account management](building-your-workflows.md#account-management-flows) flow, you'll first need to perform the following steps.‌

1. ​[Include DigitalRiver.js on your page](payments-solutions/drop-in/drop-in-integration-guide.md#step-1-include-digitalriver-js-on-your-page).
2. ​[Include the Drop-in Payments CSS file](payments-solutions/drop-in/drop-in-integration-guide.md#step-2-include-the-hydrate-css-file).
3. [​Initialize DigitalRiver.js with your public key](payments-solutions/drop-in/drop-in-integration-guide.md#step-3-initialize-digitalriver-js-with-your-public-key).
4. [​Create a container for Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-4-create-a-drop-in-payments-container).

Once you've completed these steps, you can move on to the steps specific to your workflow scenario.

## Elements prerequisites

When using [DigitalRiver.js with elements](payments-solutions/digitalriver.js/quick-start.md) to support SCA, you'll need to be using [payment sessions](../cart/payment-sessions.md), so ensure you've [completed the necessary migration](../cart/payment-sessions.md#migrating-to-payment-sessions). We also assume you are familiar with [creating and styling elements](payments-solutions/digitalriver.js/quick-start.md) as well as the [basics of capturing payment details](../general-resources/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata).

Once you've completed these prerequisites, you can perform the steps specific to your desired [purchase ](building-your-workflows.md#purchase-flows)or [account management](building-your-workflows.md#account-management-flows) scenario.

## Purchase Flows <a href="#purchase-flows" id="purchase-flows"></a>

For almost all [one-off](building-your-workflows.md#one-off), [subscription](building-your-workflows.md#subscription), and [mail-order/telephone-order (MOTO)](../cart/submitting-a-cart/initiating-a-charge.md#mail-order-telephone-order) transaction scenarios, Digital River supports [SCA-compliant](psd2-and-sca/) workflows that use either [Drop-in Payments](payments-solutions/drop-in/) or [DigitalRiver.js elements](payments-solutions/digitalriver.js/).‌

### One-off  <a href="#one-off" id="one-off"></a>

‌You can develop workflows that allow customers to [enter](building-your-workflows.md#credit-card-details-entered-by-customer-during-checkout), [save](building-your-workflows.md#credit-card-details-saved-by-customer-during-checkout), and [retrieve ](building-your-workflows.md#customer-selects-saved-credit-card-during-checkout)their payment information while making one-off purchases.&#x20;

#### Customers enter their credit card information <a href="#credit-card-details-entered-by-customer-during-checkout" id="credit-card-details-entered-by-customer-during-checkout"></a>

‌In this flow, s enter their credit card information during the checkout process.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

‌The following demonstrates how to build a workflow for this scenario using both Drop-in Payments and Elements. We also provide a [demo](https://tools.drapi.io/cm/3ds/).&#x20;

{% tabs %}
{% tab title="Drop-in Payments" %}
**Prerequisites**: Perform the [common Drop-in Payments steps](building-your-workflows.md#common-drop-in-steps).

**Step one**: [Create a cart](../cart/creating-or-updating-a-cart/) with all tax, shipping, duty, and fee amounts in a final state.

**Step two**: Retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to create an [instance of a configuration object](payments-solutions/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate).  In the configuration [`options`](payments-solutions/drop-in/drop-in-integration-guide.md#drop-in-options), set `flow` to `checkout` and [`usage`](broken-reference) to `convenience`.

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

**Step three**: Use the configuration object to [initialize Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-6-allow-the-shopper-to-interact-with-hydrate).  &#x20;

```javascript
let dropin = digitalriver.createDropin(configuration);
```

**Step four**: On your cart page, [specify a container to place Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-7-place-drop-in-payments-on-your-cart-or-shopper-page).

Drop-in Payments renders in the specified container.

![](<../.gitbook/assets/image (2) (1).png>)

Customers **** enter their credit card information and click the [configurable ](payments-solutions/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-payments-button)**Pay Now** button**.**&#x20;

If the customers completes the SCA steps necessary to make the source chargeable, then the [`onSuccess` metho](payments-solutions/drop-in/drop-in-integration-guide.md#onsuccess)d is called and Digital River returns a unique Source in a [chargeable state](broken-reference).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

A chargeable source is returned.

**Step five**: Attach the source to the cart.&#x20;

**Step six**: Create the order by submitting the cart.
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one:** Create a cart with all tax, shipping, duty, and fee amounts in a final state.

**Step two:** Retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to [create a source](../cart/payment-sessions.md#creating-a-source-with-payment-sessions).

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

\
Once the shopper provides the required SCA, a chargeable source is returned.&#x20;

**Step three:** [Attach the source to a cart](sources/using-the-source-identifier.md#attaching-sources-to-a-cart).

**Step four**: Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

#### Customers save their credit card information <a href="#credit-card-details-saved-by-customer-during-checkout" id="credit-card-details-saved-by-customer-during-checkout"></a>

In this flow, customers enter credit card information and save it to their account during a one-off transaction.&#x20;

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

The following demonstrates how to build workflows for this scenario using both Drop-in Payments and Elements. We also provide a [demo](https://tools.drapi.io/cm/drop-in/allow-save-payment?country=US).&#x20;

{% tabs %}
{% tab title="Drop-in Payments" %}
**Prerequisites**: Perform the [common Drop-in Payments steps](building-your-workflows.md#common-drop-in-steps).

**Step one**: Create a cart with all tax, shipping, duty, and fee amounts in a final state.

**Step two**: Retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to create [an instance of a configuration object](payments-solutions/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate). In the configuration [`options`](payments-solutions/drop-in/drop-in-integration-guide.md#drop-in-options), set `flow` to `checkout` and [`usage` ](payments-solutions/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use)to `convenience.` To prompt Drop-in payments to display the save payment option, set `showSavePaymentAgreement` to `true`.

You should also configure the `usage` parameter. Doing so identifies the [future use of the payment source](payments-solutions/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use).&#x20;

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        "showSavePaymentAgreement": true,
        "usage": "subscription"
    },
    ...
}

let dropin = digitalriver.createDropIn(configuration);
```

**Step three**: Use the configuration object to [initialize Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-6-allow-the-shopper-to-interact-with-hydrate).&#x20;

```javascript
let dropin = digitalriver.createDropIn(configuration);
```

**Step four**: On your cart page, [specify a container to place Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-7-place-drop-in-payments-on-your-cart-or-shopper-page).

Drop-in renders in the specified container.

![](<../.gitbook/assets/image (3).png>)

Customers enter their credit card information, select the save account and payment information option and click the [configurable ](payments-solutions/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-payments-button)**Pay Now** button**.**&#x20;

If the customers completes the SCA steps necessary to make the source chargeable, then the [`onSuccess` metho](payments-solutions/drop-in/drop-in-integration-guide.md#onsuccess)d is called and Digital River returns a unique Source in a [chargeable state](broken-reference).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

**Step five**: Attach the source to the shopper.

**Step six**: Attach the shopper to the cart.

**Step seven**: Create the order by submitting the cart.
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section. Your flow also needs to display the storage terms and provide shoppers the option of saving their payment information.&#x20;

**Step one:** Create a cart with all tax, shipping, duty and fee amounts in a final state.

**Step two:** Retrieve the [payment session identifier](broken-reference) and use it to configure the [`createSource()`](../general-resources/reference/digitalriver-object.md#creating-sources) method. The configuration object should also set `futureUse` to `true` and [`usage` ](../general-resources/reference/digitalriver-object.md#specifying-a-sources-future-use)to `convenience`. Use `mandate.terms` to pass the save payment agreement that the customer accepts.

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

Once the method is called and the customer provides the required SCA, a unique Source in a chargeable source is returned.&#x20;

**Step three**: [Attach the source to the customer](sources/using-the-source-identifier.md#attaching-sources-to-customers).

**Step four:** [Attach the source to the cart](sources/using-the-source-identifier.md#attaching-sources-to-a-cart).

**Step five**: Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

#### Customers retrieve their credit card information <a href="#customer-selects-saved-credit-card-during-checkout" id="customer-selects-saved-credit-card-during-checkout"></a>

In this one-off purchase flow, the customers select a credit card that they previously saved to their account. The key step is to call the [authenticate source method](sources/retrieving-sources.md#obtain-a-shoppers-sources).

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | No                          | Yes                 |

{% tabs %}
{% tab title="Drop-in Payments" %}
[Drop-in Payments](payments-solutions/drop-in/) do not currently support retrieving stored payment methods. In order to handle this flow, use [Elements](payments-solutions/digitalriver.js/).
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one:** Create a cart with all tax, shipping, duty, and fee amounts in a final state.

**Step two:** [Retrieve the customer's payment sources](sources/retrieving-sources.md#obtain-a-shoppers-sources) and display them to the shopper during the checkout process.

**Step three**: If the shopper selects a saved payment method, you'll need to determine whether SCA is required. To do this, call the [`authenticateSource()`](../general-resources/reference/digitalriver-object.md#authenticating-sources) method.

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

After invoking this method, Digital River automatically handles any required SCA. Once authentication is complete or is determined not to be necessary, the method resolves, allowing the checkout flow to continue.

If authentication is successful, Digital River returns the [Source ](sources/)in a [`chargeable` stat](sources/#source-state)e.

**Step four:**[ **** Attach the source to the cart](sources/using-the-source-identifier.md).

**Step five:** Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

### Subscription  <a href="#subscription" id="subscription"></a>

SCA is required for subscription acquisitions but not merchant-initiated auto-renewals. In this section, you'll find more information on developing SCA-compliant workflows for the following subscription checkout scenarios:‌

* [Shopper enters credit card details during subscription acquisition](building-your-workflows.md#customer-enters-credit-card-details-during-subscription-acquisition-checkout)
* [Shopper retrieves credit card details during subscription acquisition](building-your-workflows.md#customer-saves-credit-card-details-during-subscription-acquisition-checkout)
* [Merchant-initiated auto renewals](building-your-workflows.md#merchant-initiated-auto-renewals)

#### Shopper apply and save their credit card information during a subscription acquisition <a href="#customer-enters-credit-card-details-during-subscription-acquisition-checkout" id="customer-enters-credit-card-details-during-subscription-acquisition-checkout"></a>

In this flow, during the checkout process, shoppers use a credit card to simultaneously acquire an auto-renewing subscription and save their payment information.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| Yes           | Yes                         | Yes                 |

The following demonstrates how to build a workflow for this scenario using both Drop-in Payments and Elements.

{% tabs %}
{% tab title="Drop-in Payments" %}
**Prerequisites**: Perform the [common Drop-in Payments steps](building-your-workflows.md#common-drop-in-steps).

**Step one**: Create a cart that contains an auto-renewing subscription and all tax, shipping, duty, and fee amounts are in a final state.

**Step two**: Retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to [create an instance of a configuration object](payments-solutions/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate).  When specifying `options`, set `flow` to `checkout` , `showSavePaymenAgreement` to `true`, and `usage` to `subscription`.

**Step three**: Use the configuration object to [initialize Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-6-allow-the-shopper-to-interact-with-hydrate).

```javascript
let configuration = {
    sessionId: "d3941a36-6821-4d93-be23-6190226ae5f7",
    options: {
        "flow": "checkout",
        "showSavePaymentAgreement": true,
        "usage": "subscription"
    },
}
  
let dropin = digitalriverpayments.createDropIn(configuration);
```

**Step four**: On your cart page, [specify a container to place Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-7-place-drop-in-payments-on-your-cart-or-shopper-page).

Drop-in renders in the specified container.

![](<../.gitbook/assets/drop-in-save-payment (1) (1) (1).png>)

Shoppers **** must enter their credit card information, select the save account and payment information option and click the [configurable](payments-solutions/drop-in/drop-in-integration-guide.md#customizing-the-drop-in-button-text) **Pay Now** button**.**

**Step five**: If the shopper completes the SCA steps necessary to make the source chargeable, then [call the `onSucess` method](payments-solutions/drop-in/drop-in-integration-guide.md#the-onsuccess-event-returns-the-source).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

A chargeable source is returned that is ready for storage.

**Step six**: Attach the source to the shopper.&#x20;

**Step seven**: Attach the shopper to the cart.

**Step eight**: Create the order by submitting the cart.
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

Your flow also needs to display the storage terms and provide customers the option of saving their payment information.

**Step one**: Create a cart that contains an auto-renewing subscription and all tax, shipping, duty and fee amounts are in a final state.

**Step two:** If a shopper selects the option to save the payment method and agrees to the displayed terms, retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to [create a source](../cart/payment-sessions.md#creating-a-source-with-payment-sessions).&#x20;

The `payload` should set `futureUse` to `true`,  configure  `usage` to `subscription`, and provide the `mandate.terms` that the shopper agreed to on your storefront.&#x20;

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

Once the shopper provides the required SCA, a Source in a `chargeable` state is returned.

**Step three:** Attach the source to the shopper.

**Step four**: Attach the shopper to the cart.

**Step five:** Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

#### Shopper retrieves credit card details during subscription acquisition <a href="#customer-saves-credit-card-details-during-subscription-acquisition-checkout" id="customer-saves-credit-card-details-during-subscription-acquisition-checkout"></a>

In this flow, during the checkout process, shoppers select a credit card they previously saved to their account in order to acquire an auto-renewing subscription.

| SCA required? | Drop-in supported? | Elements supported? |
| ------------- | ------------------ | ------------------- |
| Yes           | No                 | Yes                 |

‌The following demonstrates how to build a workflow for this scenario using Elements. When building this workflow, the key step is to call the [`authenticateSource` method](../general-resources/reference/digitalriver-object.md#authenticating-sources).

{% tabs %}
{% tab title="Drop-in Payments" %}
Drop-in Payments does not currently support retrieving stored payment methods. In order to handle this flow, use Digital River with elements.
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one**: Create a cart that contains an auto-renewing subscription and all tax, shipping, duty, and fee amounts are in a final state.

**Step two:** Retrieve the shopper's payment sources and display them to the shopper during the checkout process.

**Step three**: If the shopper selects a saved payment method, you'll need to determine whether SCA is required. To do this, call the [`authenticateSource` method](../general-resources/reference/digitalriver-object.md#authenticating-sources).&#x20;

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

After invoking this method, Digital River automatically handles any required SCA. Once authentication is complete or is determined not to be necessary, the method resolves, allowing the checkout flow to continue.

A chargeable source is returned.&#x20;

**Step four:** Attach the source to a cart.

**Step five:** Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

#### Merchant-initiated auto renewals <a href="#merchant-initiated-auto-renewals" id="merchant-initiated-auto-renewals"></a>

In this flow, you initiate a subscription auto-renewal for the shopper. Although this flow type does not require SCA, you should ensure you're properly managing subscriptions, setting up auto-renewals, and initiating the charge type during the checkout process.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | N/A                         | N/A                 |

### Mail order/telephone order <a href="#mail-order-telephone-order" id="mail-order-telephone-order"></a>

SCA is not required for transactions where shoppers provide their payment details by regular mail, fax, or telephone. But mail order and telephone order (MOTO) transactions are supported by Elements.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | No                          | Yes                 |

The following demonstrates how to build a workflow for this scenario using Elements.

{% tabs %}
{% tab title="Drop-in Payments" %}
For this flow type, you should use Element to capture credit card details.&#x20;
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one**: Create a cart with all tax, shipping, duty, and fee amounts final state.

**Step two:** Retrieve the [payment session identifier](../cart/payment-sessions.md#enable-payment-sessions) from the cart, and use it to [create a source](../cart/payment-sessions.md#creating-a-source-with-payment-sessions).

Once the shopper provides the required SCA, a chargeable source is returned.

**Step three:** Attach the source to a cart.

**Step four**: Create the order by submitting the cart.
{% endtab %}
{% endtabs %}

## Account management flows <a href="#account-management-flows" id="account-management-flows"></a>

For account management flows, you only need to adhere to SCA regulations when [saving a shopper's credit card for future use](building-your-workflows.md#saving-a-credit-card-for-future-use). However, the other two scenarios, [updating a credit card's expiration date](building-your-workflows.md#updating-a-credit-cards-expiration-date) and [updating a credit's card billing address](building-your-workflows.md#updating-a-credit-cards-billing-address), while not required to have SCA, are both supported by elements.

### Saving a credit card for future use <a href="#saving-a-credit-card-for-future-use" id="saving-a-credit-card-for-future-use"></a>

In this flow, you're saving a shopper's credit card details for use in a future transaction.

For Drop-in PaymentsDrop-in Payments, the key step is to build the configuration object so that `flow` is set to `managePaymentMethods` and the`usage` parameter properly [configures the source for future use](payments-solutions/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use).&#x20;

When using Elements, your `payload`  should set `futureUse` to `true`, ensure `usage` [specifies a future use for the source](../general-resources/reference/digitalriver-object.md#specifying-a-sources-future-use), and provide the `mandate.terms` that the customer agreed to.

| SCA required? | Drop-in Payments supported? | Elements supported? |   |
| ------------- | --------------------------- | ------------------- | - |
| Yes           | Yes                         | Yes                 |   |

The following demonstrates how to build a workflow for this scenario using both Drop-in Payments and Elements. We also provide a [demo](https://tools.drapi.io/cm/drop-in/manage-payment-methods).&#x20;

{% tabs %}
{% tab title="Drop-in" %}
**Prerequisites**: Perform the [common Drop-in Payments steps](building-your-workflows.md#common-drop-in-steps).

**Step one**: You are on a page where the Customer may configure payment methods stored against their account.

**Step two**: Create an [instance of a configuration object](payments-solutions/drop-in/drop-in-integration-guide.md#step-5-configure-hydrate) that offers shoppers the ability to save payment methods on their account page.&#x20;

You should configure the `flow` parameter to allow customers to [manage their payment methods](payments-solutions/drop-in/drop-in-integration-guide.md#drop-in-options) and the  `usage` parameter to identify the [future use of the payment source](payments-solutions/drop-in/drop-in-integration-guide.md#specifying-a-sources-future-use).&#x20;

**Step three**: Use the configuration object to [initialize Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-6-allow-the-shopper-to-interact-with-hydrate).

```javascript
let configuration = {
    options: {
        "flow": "managePaymentMethods",
        "usage": "subscription"
    },
    ...
}
  
let dropin = digitalriverpayments.createDropIn(configuration);
```

**Step four**: On the account management page, [specify a container to place Drop-in Payments](payments-solutions/drop-in/drop-in-integration-guide.md#step-7-place-drop-in-payments-on-your-cart-or-shopper-page).

Drop-in renders in the specified container.

![](<../.gitbook/assets/image (4).png>)

Shoppers **** enter their credit card information, select the save account and payment information option and click the [configurable](payments-solutions/drop-in/drop-in-integration-guide.md#customizing-the-text-of-the-drop-in-payments-button) **Add Payment Method** button.&#x20;

**Step five**: If the shopper completes the SCA steps necessary to make the source chargeable, then [call the `onSucess` method](payments-solutions/drop-in/drop-in-integration-guide.md#the-onsuccess-event-returns-the-source).

```javascript
...
onSuccess: function (data) { doSometingWithTheSource(data) },
...
```

A chargeable source is returned that is [ready for storage](payments-solutions/drop-in/drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details).&#x20;

**Step six**: Attach the source to the shopper.
{% endtab %}

{% tab title="DigitalRiver.js with  elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section. Your flow also needs to display the storage terms and provide shoppers the option of saving their payment information.

**Step one**: If a customer selects the option to save a payment method and agrees to the displayed terms, the `payload` should set `futureUse` to `true`,  configure  `usage` to identify the [future use of the payment source](../general-resources/reference/digitalriver-object.md#specifying-a-sources-future-use), and provide the `mandate.terms` that the customer agreed to on your storefront.&#x20;

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

Once the shopper provides the required SCA, a chargeable source is returned.

**Step three:** Attach the source to the shopper.
{% endtab %}
{% endtabs %}

### Updating a credit card's expiration date

In this flow, you're updating the expiration date on a shopper's saved credit card.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | No                          | Yes                 |

The following demonstrates how to build a workflow for this scenario using Elements.

{% tabs %}
{% tab title="Drop-in Payments" %}
Drop-in Payments does not support interacting directly with saved payment methods‌
{% endtab %}

{% tab title="Digital River with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one:** Retrieve the shopper's payment sources and display them to the shopper.\
\
The shopper selects the payment method to update.&#x20;

**Step two:** Capture the updated expiration date from the shopper and pass it to the [update source](../general-resources/reference/digitalriver-object.md#digitalriver-updatesource-element-sourcedata) method.
{% endtab %}
{% endtabs %}

### Updating a credit card's billing address

In this flow, you're updating the billing address on a shopper's saved credit card.

| SCA required? | Drop-in Payments supported? | Elements supported? |
| ------------- | --------------------------- | ------------------- |
| No            | No                          | Yes                 |

The following demonstrates how to build a workflow for this scenario using Elements.

{% tabs %}
{% tab title="Drop-in Payments" %}
Drop-in Payments does not support interacting directly with saved payment methods‌
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
**Prerequisites**: Refer to the [Elements prerequisites](building-your-workflows.md#elements-prerequisites) section.&#x20;

**Step one:** Retrieve the shopper's payment sources and display them to the shopper.\
\
The shopper selects the payment method to update.&#x20;

**Step two:** Capture the updated billing address from the shopper and pass it to the [update source](../general-resources/reference/digitalriver-object.md#digitalriver-updatesource-element-sourcedata) method.
{% endtab %}
{% endtabs %}
