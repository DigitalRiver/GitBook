---
description: Learn the basics of payment sessions
---

# Payment sessions

A payment session tracks a transaction's payment. On this page, you'll find information on:

* [The benefits of using payment sessions](payment-sessions.md#why-use-payment-sessions)
* [When to use payment sessions](payment-sessions.md#when-to-use-payment-sessions)
* [The payment session object](payment-sessions.md#the-payment-session-object)
* [How to migrate to payment sessions](payment-sessions.md#migrating-to-payment-sessions)

## Why use payment sessions?

Payment sessions allow you to [gain access to Drop-in payments](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md). This solution lessens your front-end development burden. To take just one example, [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) automatically retrieves a transaction's applicable [payment methods](../../../payments/supported-payment-methods/) and then presents them to customers during the payment collection stage of a checkout.

Additionally, payment sessions simplify [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) creation. Without them, you'll need to retrieve numerous data points from the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and ensure they're properly formatted before passing them to [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#createsource-element-sourcedata). With payment sessions however you simply retrieve the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session.id` and then pass that value to the appropriate [source creation method](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources), thereby minimizing your data transfer requirements

Payment sessions also allow you to comply with [PSD2 and SCA](../../../payments/psd2-and-sca/) regulations. If you reference this object when creating [credit card sources](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/credit-cards.md), Digital River, when necessary, automatically collects a customer's authentication data.

## When to use payment sessions

You can use payment sessions to:

* [Configure various elements](payment-sessions.md#configure-elements)
* [Retrieve available payment methods](payment-sessions.md#retrieve-available-payment-methods)
* [Create sources](payment-sessions.md#creating-a-source-with-payment-sessions)
* [Determine when to create orders](payment-sessions.md#how-to-determine-when-to-create-an-order)
* [Determine the next action to take after order creation](payment-sessions.md#determine-next-action)

### Configure elements

The following [elements](../../../developer-resources/reference/elements/) all can be configured with a payment session identifier:

* [iDeal](../../../developer-resources/reference/elements/ideal-element.md)
* [Tax identifier](../../../developer-resources/reference/elements/tax-identifier-element.md)
* [Invoice attribute](../../../developer-resources/reference/elements/invoice-attribute-element.md)
* [PayPal](../../../developer-resources/reference/elements/paypal-elements.md)

### Retrieve available payment methods

If you're using [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/) to collect payment, you can call [`retrieveAvailablePaymentMethods()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#retrieving-available-payment-methods) to get a transaction's applicable payment methods and then present them as options during checkouts.&#x20;

To configure this method, retrieve the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session.id` and pass it to `sessionId`.&#x20;

```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f"
}).then(function(result) {
    //do something with the data
});
```

### Create sources <a href="#creating-a-source-with-payment-sessions" id="creating-a-source-with-payment-sessions"></a>

Both of Digital River's [source creation methods](../../../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) can be configured with the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session.id`. The data our payment service needs to create the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is then retrieved from that referenced object.

{% tabs %}
{% tab title="Drop-in payments" %}
```javascript
let configuration = {
    "sessionId": "172deb0f-de6f-4d2c-9555-53f3894b6318",
    "options": {
        "flow": "checkout",
        "showComplianceSection": true
    }, 
    onSuccess: function(data) {}, 
    onError: function(data) {}, 
    onReady: function(data) {}, 
    onCancel: function(data) {}
}
                                    
let dropin = digitalriverpayments.createDropin(configuration);
dropin.mount("drop-in");
```
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
```javascript
let payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "type": "payPal",
    "payPal": {
        "returnUrl": "https://mywebsite.com/paymentCallBack.html",
        "cancelUrl": "https://mywebsite.com/paymentCallBack.html"
    }
}

digitalriver.createSource(payload).then(function(result) {
    if(result.state === "chargeable") {
        sendToBackEnd(result);
    } else {
        doErrorScenario();
    }
});
```
{% endtab %}
{% endtabs %}

### Determine when to create orders <a href="#how-to-determine-when-to-create-an-order" id="how-to-determine-when-to-create-an-order"></a>

Before [creating an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session` should be in a [`state`](payment-sessions.md#session-state) of `requires_confirmation` and its [`amountRemainingToBeContributed`](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed) should be `0`.&#x20;

{% code title="Checkout" %}
```javascript
{
    "id": "8f349290-a6ec-438a-8623-ca0c6e6f65fa",
    ...
    "payment": {
        ...
        "session": {
            "id": "1403a59f-37a8-4d9e-8e13-838cf6f2a0cc",
            "amountContributed": 27.01,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "1403a59f-37a8-4d9e-8e13-838cf6f2a0cc_a2a14087-2aa7-4876-b4f9-d16b5ae6817b"
        }
    }
}
```
{% endcode %}

### Determine next action

If you [create an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) and its [`state`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events) is `pending_payment`, then this indicates that the [charge](../../../order-management/orders/payment-charges/) on the [primary payment `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#primary-versus-secondary-sources) isn't authorized and the goods shouldn't be fulfilled yet.

To handle this `state` change event, check the value of the order's [`payment.session.nextAction.action`](payment-sessions.md#next-action).

* If it's `redirect`, refer to [Handling redirect payment methods](../building-you-workflows/handling-redirect-payment-methods.md).
* If it's `show_payment_instructions`, refer to [Handling delayed payment methods](../building-you-workflows/handling-delayed-payment-methods.md).

## The payment session object

{% hint style="warning" %}
The attributes described in this section are only contained in [versions](../../../general-resources/versioning.md) `2021-03-23` and higher.
{% endhint %}

The following section provides information on a payment session object's:

* [`state`](payment-sessions.md#session-state)
* [`amountContributed` and `amountRemainingToBeContributed`](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed)
* [`nextAction`](payment-sessions.md#next-action)

### Session state

A payment session has a defined lifecycle. Each stage of that lifecycle is represented by a `state`. When building your integration, we recommend you pay close attention to:

* [`requires_source`](payment-sessions.md#requires\_source)
* [`requires_confirmation`](payment-sessions.md#requires\_confirmation)
* [`pending_redirect`](payment-sessions.md#pending-redirect)
* [`pending_funds`](payment-sessions.md#pending\_funds)
* [`pending`](payment-sessions.md#pending)
* [`complete`](payment-sessions.md#complete)

For a complete list of payment session `state` values, refer to the [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), or [invoices](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) API reference documentation.&#x20;

#### `requires_source`

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session.state` is `requires_source`, then this indicates that either:&#x20;

* No [primary `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) is associated with the checkout or
* The aggregated `amount` of any [secondary `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#secondary-payment-sources) associated with the checkout is less than the checkout's `totalAmount`.

In both cases, Digital River won't be able to generate an aggregated `amount` of [`charges[]`](../../../order-management/orders/payment-charges/) large enough to cover the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `totalAmount`. As a result, the [`amountRemainingToContribute`](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed) remains greater than `0.0` and any attempt to [create an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) is blocked.

#### `requires_confirmation`

When the payment session's `state` is `requires_confirmation`, then one or more [`sources[]`](../../../payments/payment-sources/) have been applied to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and their aggregated `amount` is sufficient to fund the transaction.&#x20;

The [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session.state` must be `requires_confirmation` before you [create the order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). &#x20;

For example, if you [attach](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) a [primary source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) to a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), then the [`amountRemainingToContribute`](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed) drops to `0.0` and the payment session's `state` transitions to `requires_confirmation`.

#### `pending_redirect`

A payment session in a `state` of `pending_redirect` indicates that customers were successfully redirected to the payment provider's portal but have yet to complete the actions necessary to authorize payment.&#x20;

This `state` only occurs when customers choose a [payment method](../../../payments/supported-payment-methods/) whose resulting [source](../../../payments/payment-sources/) has a [`redirect` authentication `flow`](../../../payments/payment-sources/#authentication-flow).

If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `payment.session.state` persists as `pending_redirect`, then customers either selected the cancel payment option or clicked their web browser's back button.

#### `pending_funds`

A payment session `state` of `pending_funds` indicates that customers must complete an asynchronous process before payment is authorized.&#x20;

This `state` occurs when customers choose a [payment method](../../../payments/supported-payment-methods/) whose resulting [source](../../../payments/payment-sources/) has a [`receiver` authentication `flow`](../../../payments/payment-sources/#authentication-flow).

For example, an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) with a [`payment.sources[].type`](../../../payments/payment-sources/#supported-payment-methods) of [`konbini`](../../../payments/supported-payment-methods/konbini.md) and a `payment.session.state` of `pending_funds` means that customers have yet to complete payment at the designated convenience store (e.g. 7-11 or FamilyMart).

#### `pending`

A `pending` payment session `state` means that customers have completed all the necessary actions (such as [SCA](../../../payments/psd2-and-sca/) and redirects) but certain back-end payment processes remain incomplete.

#### `complete`

Once all of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) payment [`charges[]`](../../../order-management/orders/payment-charges/) are [`capturable`](../../../order-management/orders/payment-charges/#the-charge-lifecycle), its `payment.session.state` typically transitions to `complete`.

### Amount contributed and remaining <a href="#amount-contributed-and-amount-remaining-to-be-contributed" id="amount-contributed-and-amount-remaining-to-be-contributed"></a>

Once you associate a [primary payment `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), Digital River uses it to fund the transaction in full and `payment.session.amountRemainingToContribute` drops to `0.0`.

But when checkouts only contain [secondary payment `sources[]`](../../../payments/payment-sources/using-the-source-identifier.md#secondary-payment-sources), you need to confirm that sufficient funds exist to cover the checkout's `totalAmount`. If this isn't the case, and you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you receive the following error:

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "order_submit_failed",
            "message": "Payment session status is invalid."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

By comparing values in the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `payment.session`, you can determine how much additional funding, if any, is required. The `amountContributed` represents the aggregated `amount` of all the checkout's `payment.sources[]`. The `amountRemainingToBeContributed` is how much is needed to fund the transaction.

If `amountContributed` is equal to the checkout's `totalAmount` or the `amountRemainingToBeContributed` is `0.0`, then you don't need to request any more payment methods from the customer, and, once the payment session's [`state`](payment-sessions.md#session-state) is [`requires_confirmation`](payment-sessions.md#requires-confirmation), you can [create the order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

But if `amountContributed` is less than the checkout's `totalAmount` or `amountRemainingToBeContributed` is greater than `0.0`, then the customer needs to supply additional payment methods before you [create the order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). This only happens however when you have yet to associate a [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) with the checkout. Once that's done, `amountRemainingToBeContributed` drops to `0.0`.

### Next action

If customers opt to fund a transaction with a [payment method](../../../payments/supported-payment-methods/) whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has an authentication [`flow`](../../../payments/payment-sources/#authentication-flow) of `redirect` or `receiver`, then, after you [associate the source with the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) and submit the [create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), in most cases, will contain `payment.session.nextAction` and this object's nested `action` will be either `redirect` or `show_payment_instructions`.

{% tabs %}
{% tab title="redirect" %}
If `action` is `redirect`, then send customers to the address specified by `data.redirectUrl`. For details, refer to [Handling redirect payment methods](../building-you-workflows/handling-redirect-payment-methods.md).

{% code title="Order" %}
```json
{
    "id": "240354510336",
    ...
    "payment": {
        ...
        "session": {
            "id": "1b682138-ce9f-46ec-8b5e-94b710128cd9",
            ...
            "nextAction": {
                "action": "redirect",
                "data": {
                    "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/3fab742c-a7e8-4a90-8951-86d071fa070d?apiKey=pk_test_a45b91ba4f984df7a229b2ab5941ce1c"
                }
            }
        }
    },
    ...
}
```
{% endcode %}
{% endtab %}

{% tab title="show_payment_instructions" %}
If `action` is `show_payment_instructions` then use `data.sourceId` and `data.sourceClientSecret` to configure the [delayed payment instructions element](../../../developer-resources/reference/elements/delayed-payment-instructions-element.md). For details, refer to [Handling delayed payment methods](../building-you-workflows/handling-delayed-payment-methods.md).

{% code title="Order" %}
```json
{
    "id": "239809940336",
    ...
    "payment": {
        ...
        "session": {
            "id": "afaed310-419f-4ced-912c-6830a98c7384",
            ...
            "nextAction": {
                "action": "show_payment_instructions",
                "data": {
                    "sourceId": "9c00d78c-dbad-4303-b366-7e0a49c322e7",
                    "sourceClientSecret": "9c00d78c-dbad-4303-b366-7e0a49c322e7_246ed54a-0dfc-41f0-9e98-14036adf642e"
                }
            }
        }
    },
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Migrating to payment sessions

If you collect payment by using [DigitalRiver.js with elements](../../../payments/payment-integrations-1/digitalriver.js/), and you're not currently using payment sessions, but want to migrate to this solution, then the conversion process is fairly straightforward.&#x20;

{% hint style="success" %}
To collect payment, we generally recommend that you use [Drop-in payments](../../../payments/payment-integrations-1/drop-in/).
{% endhint %}

In the Digital River APIs, payment sessions are automatically enabled. This means that each time you [create a checkout](./#creating-and-updating-the-checkout), the response contains a payment session identifier that you use to configure [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources).

### Update your code

You'll need to update your code to integrate with payment sessions. For each of your enabled [payment methods](../../../payments/supported-payment-methods/), add `sessionId` to the payload that gets passed to [`createSource()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources).

You'll also need to remove some parameters. The specific parameters that must be removed depends on the payment method.

For each payment method, you can find instructions and example code in the following sections: [Credit Card](payment-sessions.md#credit-card), [PayPal](payment-sessions.md#paypal), [PayPal Billing](payment-sessions.md#paypal-billling), [PayPal Credit](payment-sessions.md#paypal-credit), [SEPA Direct Debit](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/direct-debit.md), [Wire Transfer](payment-sessions.md#wire-transfer), [Cash on Delivery - Japan](payment-sessions.md#cash-on-delivery-japan), [Payco - Korea Payments](payment-sessions.md#payco-korea-payments), [Bank Transfer - Korea Payments](payment-sessions.md#bank-transfer-korea-payments), [Online Banking - IBP](payment-sessions.md#online-banking-ibp), [bPay](payment-sessions.md#bpay), [Konbini](payment-sessions.md#konbini), [Klarna](payment-sessions.md#klarna), [Klarna Recurring](payment-sessions.md#klarna-recurring), [TreviPay](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/trevipay.md).

#### Credit Card

For credit cards, you add `sessionId` to the payload but do not remove any existing parameters.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "creditCard",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "john.doe@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "10380 Bren Road West",
            line2: "Suite 123",
            city: "Minnetonka",
            state: "MN",
            postalCode: "55343",
            country: "US"
        }
    }
}

digitalriver.createSource(cardCVV, payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "type": "creditCard",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "john.doe@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "10380 Bren Road West",
            line2: "Suite 123",
            city: "Minnetonka",
            state: "MN",
            postalCode: "55343",
            country: "US"
        }
    }
}

digitalriver.createSource(cardCVV, payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### PayPal

For PayPal, you add `sessionId` to the payload and remove `amount`, `currency`, `payPal.items`, `payPal.taxAmount`, `payPal.shippingAmount`, `payPal.amountsEstimated`, `payPal.requestShipping`, and `payPal.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPal",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPal",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
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
{% endtab %}
{% endtabs %}

#### PayPal Billing

For PayPal Billing, you add `sessionId` to the payload and remove `amount`, `currency`, `payPalBilling.items`, `payPalBilling.taxAmount`, `payPalBilling.shippingAmount`, `payPalBilling.amountsEstimated`, `payPalBilling.requestShipping`, and `payPalBilling.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPalBilling",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPalBilling",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
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
{% endtab %}
{% endtabs %}

#### PayPal Credit

For PayPal Credit, you add `sessionId` to the payload and remove `amount`, `currency`, `payPal.items`, `payPal.taxAmount`, `payPal.shippingAmount`, `payPal.amountsEstimated`, `payPal.requestShipping`, and `payPal.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPalCredit",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPalCredit",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
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
{% endtab %}
{% endtabs %}

#### SEPA Direct Debit

For SEPA Direct Debit, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "directDebit",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "directDebit": {
        "returnUrl": "https://mypage.com"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "directDebit",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "directDebit": {
        "returnUrl": "https://mypage.com"
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
{% endtab %}
{% endtabs %}

#### Wire Transfer

For Wire Transfer, you add `sessionId`to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "wireTransfer",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "wireTransfer": {
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var data = {
    "type": "wireTransfer",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "wireTransfer": {
    }
}

digitalriver.createSource(data).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Cash on Delivery - Japan

For Cash on Delivery - Japan, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "codJapan",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "codJapan": {
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "codJapan",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "codJapan": {
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
{% endtab %}
{% endtabs %}

#### Payco - Korea Payments

For Payco - Korea Payments, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "payco",
    "amount": 100,
    "currency": "KRW",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "payco": {
        "returnUrl": "https://yourReturnUrl.com"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payco",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "payco": {
        "returnUrl": "https://yourReturnUrl.com"
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
{% endtab %}
{% endtabs %}

#### Bank Transfer - Korea Payments

For Bank Transfer - Korea Payments, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "bankTransfer",
    "amount": 100,
    "currency": "KRW",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "bankTransfer": {
        "returnUrl": "https://yourReturnUrl.com"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "bankTransfer",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "bankTransfer": {
        "returnUrl": "https://yourReturnUrl.com"
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
{% endtab %}
{% endtabs %}

#### Online Banking - IBP

For Online Banking - IBP, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "onlineBanking",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "52-58 Neue Mainzer Straße",
                "line2": "",
                "city": "Frankfurt am Main",
                "state": "HE",
                "postalCode": "60311",
                "country": "DE"
            }
        },
        "onlineBanking": {
            "returnUrl": "https://myurl.com/success",
            "cancelUrl": "https://myurl.com/cancel",
            "bankCode": "82"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "onlineBanking",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "52-58 Neue Mainzer Straße",
                "line2": "",
                "city": "Frankfurt am Main",
                "state": "HE",
                "postalCode": "60311",
                "country": "DE"
            }
        },
        "onlineBanking": {
            "returnUrl": "https://myurl.com/success",
            "cancelUrl": "https://myurl.com/cancel",
            "bankCode": "82"
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
{% endtab %}
{% endtabs %}

#### Konbini

For Konbini, you add `sessionId` to the payload and remove `amount` and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "konbini",
    "amount": 120.99,
     "currency": "JPY",
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "konbini",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
         "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
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
{% endtab %}
{% endtabs %}

#### Klarna

For Klarna, you add `sessionId` to the payload and remove `amount`, `currency`, `klarnaCredit.items`, `klarnaCredit.locale`, `klarnaCredit.discountAmount`, `klarnaCredit.taxAmount`, `klarnaCredit.shippingAmount`, `klarnaCredit.shipping`, `klarnaCredit.accountId`, `klarnaCredit.accountCreatedDate`, `klarnaCredit.accountUpdatedDate`, `klarnaCredit.hasPaidBefore`, `klarnaCredit.subscriptionDescription`, `klarnaCredit.subscriptionStartDate`, `klarnaCredit.subscriptionEndDate`, `klarnaCredit.autoRenewal`, and `klarnaCredit.affiliateName`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "klarnaCredit",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "email@email.org",
        "phoneNumber": "9522253720",
        "address": {
            "line1": "line1",
            "line2": "line2",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55410"
        }
    },
    "amount": "101.50",
    "currency": "USD",
    "klarnaCredit": {
        "returnUrl": "http://example.com/return",
        "cancelUrl": "http://example.com/cancel",
        "taxAmount": 0,
        "shippingAmount": 5.75,
        "items": [{
            "name": "Happy Ball",
            "quantity": "1",
            "unitAmount": "94.25",
            "subscriptionInfo": {
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "name": "Happy Ball1",
            "quantity": "2",
            "unitAmount": "0.75"
        }],
        "locale": "en_US",
        "shipping": {
            "recipient": "Guy Incognito",
            "phoneNumber": "9522253720",
            "address": {
                "line1": "line1",
                "line2": "line2",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55410"
            },
            "email": "test_email@email.org"
        },
        "accountId": "456789",
        "accountCreatedDate": "2020-11-24T15:20:00.000Z",
        "accountUpdatedDate": "2012-11-25T15:30:00.001Z",
        "hasPaidBefore": false,
        "subscriptionDescription": "Klarna Credit Recurring",
        "subscriptionStartDate": "2019-10-24T15:00:00.030Z",
        "subscriptionEndDate": "2021-10-24T15:00:00.030Z",
        "autoRenewal": "false",
        "affiliateName": "Sample Affiliate"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
  "type" : "klarnaCredit",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCredit" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
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
{% endtab %}
{% endtabs %}

#### Klarna Recurring

For Klarna Recurring, you add `sessionId` to the payload and remove `amount`, `currency`, `klarnaCreditRecurring.items`, `klarnaCreditRecurring.locale`, `klarnaCreditRecurring.discountAmount`, `klarnaCreditRecurring.taxAmount`, `klarnaCreditRecurring.shippingAmount`, `klarnaCreditRecurring.shipping`, `klarnaCreditRecurring.accountId`, `klarnaCreditRecurring.accountCreatedDate`, `klarnaCreditRecurring.accountUpdatedDate`, `klarnaCreditRecurring.hasPaidBefore`, `klarnaCreditRecurring.subscriptionDescription`, `klarnaCreditRecurring.subscriptionStartDate`, `klarnaCreditRecurring.subscriptionEndDate`, `klarnaCreditRecurring.autoRenewal`, and `klarnaCreditRecurring.affiliateName`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "klarnaCreditRecurring",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "email@email.org",
        "phoneNumber": "9522253720",
        "address": {
            "line1": "line1",
            "line2": "line2",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55410"
        }
    },
    "amount": "101.50",
    "currency": "USD",
    "klarnaCreditRecurring": {
        "returnUrl": "http://example.com/return",
        "cancelUrl": "http://example.com/cancel",
        "taxAmount": 0,
        "shippingAmount": 5.75,
        "items": [{
            "name": "Happy Ball",
            "quantity": "1",
            "unitAmount": "94.25",
            "subscriptionInfo": {
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "name": "Happy Ball1",
            "quantity": "2",
            "unitAmount": "0.75"
        }],
        "locale": "en_US",
        "shipping": {
            "recipient": "Guy Incognito",
            "phoneNumber": "9522253720",
            "address": {
                "line1": "line1",
                "line2": "line2",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55410"
            },
            "email": "test_email@email.org"
        },
        "accountId": "456789",
        "accountCreatedDate": "2020-11-24T15:20:00.000Z",
        "accountUpdatedDate": "2012-11-25T15:30:00.001Z",
        "hasPaidBefore": false,
        "subscriptionDescription": "Klarna Credit Recurring",
        "subscriptionStartDate": "2019-10-24T15:00:00.030Z",
        "subscriptionEndDate": "2021-10-24T15:00:00.030Z",
        "autoRenewal": "false",
        "affiliateName": "Sample Affiliate"
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
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
  "type" : "klarnaCreditRecurring",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCreditRecurring" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
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
{% endtab %}
{% endtabs %}
