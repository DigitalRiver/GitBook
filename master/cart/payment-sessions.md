---
description: Learn the basics of payment sessions and how to migrate your integration.
---

# Payment sessions

A payment session tracks a customer's payment throughout the checkout process. Although you're not required to, we highly [recommend you use payment sessions](payment-sessions.md#why-use-payment-sessions) to reduce the complexity of building DigitalRiver.js payment collection flows and to comply with [PSD2 and SCA](../../payments/psd2-and-sca/) regulations.&#x20;

[Migrating to payment sessions](payment-sessions.md#migrating-to-payment-sessions) is relatively straightforward and mostly involves [updating the code](payment-sessions.md#update-your-code) for each of your approved payment methods.

## Why use payment sessions?

Payment sessions allow you to comply with [PSD2 and SCA](../../payments/psd2-and-sca/) regulations. When using payment sessions to [create credit card sources](payment-sessions.md#credit-card), Digital River automatically collects the required authentication data from the customer PSD2 transactions.

Payment sessions also simplify source creation by reducing the data you're required to provide. If you don't use payment sessions, you'll need to copy numerous data points returned in the cart and ensure it is properly formatted before passing them to the [create source method](../../general-resources/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata). &#x20;

When [creating a source with payment sessions](payment-sessions.md#creating-a-source-with-payment-sessions), however, you can provide the unique identifier of the session, thereby minimizing the data you must transfer.&#x20;

Payment sessions also allow you to [gain access to Drop-in Payments](../../payments/payments-solutions/drop-in/drop-in-integration-guide.md), which lessens your front-end development burden. For each transaction, [Drop-in Payments](../../payments/payments-solutions/drop-in/) [retrieve the available payment methods](payment-sessions.md#retrieving-available-payment-methods), that are applicable to the transaction and display them as options to customers.

## Creating a source with payment sessions

When [creating a payment source,](../../payments/sources/using-the-source-identifier.md#creating-payment-sources) specify the `sessionId` in the payload that you pass to the DigitalRiver.js [create source method](../../general-resources/reference/digitalriver-object.md#creating-sources). The data needed by our payment services to create the source is then retrieved from that session.

{% tabs %}
{% tab title="Drop-in payments" %}
{% code overflow="wrap" %}
```json
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
{% endcode %}
{% endtab %}

{% tab title="DigitalRiver.js with elements" %}
{% code overflow="wrap" %}
```json
let payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "type": "payPal",
    "payPal": {
        "returnUrl": "https://yourReturnUrl.com",
        "cancelUrl": "https://yourCancelUrl.com"
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
{% endcode %}
{% endtab %}
{% endtabs %}

## How to determine when to create an order

A cart's `payment.session` can be used to determine when to create an order. Specifically, we provide you information on the [payment session's state](payment-sessions.md#session-state) as well as the [amount contributed and amount remaining to be contributed](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed).

{% code title="Cart" overflow="wrap" %}
```json
{
"    id": "47278010023",
.    ..
    "paymentSession": 
    {
        "id": "string",
        "status": "string",
        "clientSecret": "string",
        "redirectUrl": "https://api.digitalriver.com:80/payments/redirects/12759bb0-xxxx-4bdb-bfeb-9095ba8059fc?apiKey=a88fxxxx1eef47eb95bc609c22e593c8",
        "amountContributed": 
        {},
        "amountRemainingToBeContributed": 
        {}
    }
}
```
{% endcode %}

### Session state

The following are the payment session states most important when building your integration:

* [Requires confirmation](payment-sessions.md#requires-confirmation)
* [Requires source](payment-sessions.md#requires-source)
* [Complete](payment-sessions.md#complete)

#### Requires confirmation

The cart's `payment.session.state` must be `requires_confirmation` before you convert that cart to an order.

This `state` indicates that the cart's payment sources\[] are sufficient to fund the transaction. For example, when you [attach ](../../payments/sources/using-the-source-identifier.md#attaching-sources-to-a-cart)a [`chargeable` ](../../payments/sources/#source-state)[primary source](../../payments/sources/using-the-source-identifier.md#primary-payment-sources) to a checkout, the [amount remaining to contribute](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed) drops to zero, and the session's `state` transitions to `requires_confirmation`.

#### Requires source

A cart's `payment.session.state` can be `requires_source` for either of the following reasons:

* No [primary ](../../payments/sources/using-the-source-identifier.md#primary-payment-sources)or [secondary payment sources](../../payments/sources/using-the-source-identifier.md#secondary-payment-sources) have yet been applied.
* No primary payment source is applied and there are not enough [secondary payment sources](../../payments/sources/using-the-source-identifier.md#secondary-payment-sources) such as [store credit](../consumer-browsing-experience-1/common-use-cases/applying-store-credit.md) to fully fund the transaction.

In both of these scenarios, we won't be able to generate a charge amount large enough to cover the checkout's `totalAmount`. So the [amount remaining to contribute](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed) remains greater than zero and any attempt to create an order is blocked.

#### Complete

The payment session `state` typically transitions to `complete` once the order is created.

### Amount contributed and amount remaining to be contributed

Once a [primary payment source](../../payments/sources/using-the-source-identifier.md#primary-payment-sources) is attached to a cart, we use it to fully fund the transaction.

But when only [secondary payment sources](broken-reference) are attached, you need to confirm sufficient funds exist to cover the [cart's ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts)`totalAmount`. If this isn't the case, when you convert the cart to an order, you receive the following error:

{% tabs %}
{% tab title="400 Bad Request" %}
{% code overflow="wrap" %}
```json
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
{% endcode %}
{% endtab %}
{% endtabs %}

By comparing values in the cart's `payment.session`, you can determine how much additional funding, if any, is still required. The `amountContributed` represents the aggregated amount of all the cart's `payment.sources[]`. The `amountRemainingToBeContributed` is how much is needed to fully fund the transaction.

If the `amountContributed` is equal to the cart's `totalAmount` or the `amountRemainingToBeContributed` is zero, then you don't need to request any more payment methods from the customer. This means that once the [payment session is in the correct state](payment-sessions.md#session-state), and all [address requirements](removing-a-specific-applied-offer/providing-address-information.md) are met, you can convert the cart to an order.

But if the `amountContributed` is less than the cart's `totalAmount` or the `amountRemainingToBeContributed` is greater than zero, then the customer needs to supply additional payment methods before an order can be successfully created. However, this will only be the case when a [primary payment source](../../payments/sources/using-the-source-identifier.md#primary-payment-sources) is not yet attached to the checkout. Once that's done, we use it to fully fund the transaction and `amountRemainingToBeContributed` drops to zero.

## Attaching a source

You can [attach a source to a customer](../../payments/sources/#attaching-a-payment-method-to-an-order-or-cart), or [an order or cart](../../payments/sources/#attaching-a-payment-method-to-an-order-or-cart). See [Source basics](../../payments/sources/) for more information.

## Retrieving available payment methods

In DigitalRiver.js, you can use the payment session identifier to [return the payment methods available for each transaction](../../general-resources/reference/digitalriver-object.md#retrieving-available-payment-methods) and present them to the customer during the checkout process.

The method also returns the data required to use one-click payment methods like Apple Pay and Google Pay, as well as the data needed to retrieve compliance information via the DigitalRiver.js [compliance methods](../../general-resources/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale).&#x20;

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```json
digitalriver.retrieveAvailablePaymentMethods({
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f"
}).then(function(result) {
    //do something with the data
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Migrating to payment sessions

Although we generally recommend that you use [Drop-in Payments](../../payments/payments-solutions/drop-in/) to handle payments, you can also migrate your existing integration directly to payment sessions. For the Commerce API, [payment sessions must be enabled](payment-sessions.md#enable-payment-sessions).

Once you have completed this migration process, you'll need to [build your SCA workflows](../../payments/building-your-workflows.md) using [Drop-in Payments](../../payments/payments-solutions/drop-in/) or [DigitalRiver.js with elements](../../payments/payments-solutions/digitalriver.js/).&#x20;

