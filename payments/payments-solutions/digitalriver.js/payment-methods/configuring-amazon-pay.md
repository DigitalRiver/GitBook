---
description: Learn how to configure Amazon Pay for DigitalRiver.js with Elements
---

# Configuring Amazon Pay

If you're using[ DigitalRiver.js with Elements](../), you can create an [Amazon Pay](../../../supported-payment-methods/amazon-pay.md) payment method for your app or website in two easy steps:

* [Step 1: Create an Amazon Pay source using DigitalRiver.js](configuring-amazon-pay.md#step-1-create-a-google-pay-source-using-digital-river.js)
* [Step 2: Use the authorized source](configuring-amazon-pay.md#step-3-use-the-authorized-source)

## Step 1: Create an Amazon Pay source using Digital River.js

Amazon Pay is different from other payment methods. The shopper's payment information is pulled into the cart directly from their Amazon Pay account.

To create an Amazon Pay payment source, follow the instructions in the [DigitalRiver.js reference guide](../../../../general-resources/reference/). If the shopper is paying for a subscription, you must [provide the `mandate.terms`](../../../building-your-workflows.md#digitalriver.js-with-elements) that the customer agreed to on your storefront [and set `autoRenewal` to `true`](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-subscription-information.md#auto-renewal), and [`futureUse` to `true`](../../../building-your-workflows.md#saving-a-credit-card-for-future-use).

### Create an Amazon Pay element

After setting up your library per the [DigitalRiver.js reference guide](../../../../general-resources/reference/), [create an Amazon Pay element](../../../../general-resources/reference/elements/amazon-pay-element.md#creating-an-amazon-pay-element) with any customizations you would like to apply.&#x20;

{% code overflow="wrap" %}
```javascript
var options = {
    style: {
        color: 'DarkGray', // one of ['Gold', 'LightGray', 'DarkGray']
        height: '100px'
    },
    sourceData: {
        type: 'amazonPay',
        sessionId: sessionId,
        country: 'US', // required if your session does not contain shopper country
        futureUse: true, // required if you intend to use for recurring billing
        usage: 'subscription', //only required if futureUse is true - should be one of ['subscription', 'convenience', ]
        mandate: { // required for recurring/reusable
            terms: 'Yes, please save this account and payment information for future purchases.'
        }
    },
    amazonPay: {
        //Amazon Pay will redirect to this URL after the buyer signs in
        returnUrl: '<return.com URL>', 
        //where the shopper will be returned after authorizing at Amazon Pay (NOTE TO GALE: I'm not sure if this wording is right, you may want to verify with Product or Payment Service)
        resultReturnUrl: 'https://<resultreturn.com URL>', 
        //Amazon Pay will redirect to this URL if the buyer cancels sign-in on the Amazon Pay hosted page
        cancelUrl: '<cancel.com URL>', 
        // Placement of the Amazon Pay button on your website. One of ['Home', 'Cart', 'Product', 'Checkout', 'Other']
        placement: 'Product', 
            // optional, one of ['en_US', 'en_GB', 'de_DE', 'fr_FR', 'it_IT', 'es_ES', 'ja_JP']
        checkoutLanguage: 'fr_FR'
    }
    }
};

var amazonpay = digitalriver.createElement('amazonpay', options);
amazonpay.mount('amazonpay');
```
{% endcode %}

| Attribute          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `country`          | An optional string that represents an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code. This is required when your session does not contain a shopper country.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `returnUrl`        | <p>A redirect to the Amazon Pay Sign in page. </p><p>When the shopper selects Amazon Pay as their payment method from the cart (see callout 1 in the image below), Digital River creates a payment session and source and redirects the shopper to the Amazon Pay Sign in page (see callout 2). The shopper must sign in to Amazon to access the order confirmation page. At this point, the payment information is attached to the Digital River payment source. The shopper must complete the verification process and place the order (see callout 3). Amazon Pay processes the payment (see callout 4) and the source is attached to the cart.</p> |
| `resultReturnUrl`  | <p>A redirect to your thank you page.</p><p>After Amazon Pay process the payment, the shopper is redirected to your thank you page (see callout 5).</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `cancelUrl`        | <p>A redirect from the cancelled login page to a page specified by you.<br>Amazon will redirect the shopper to this cancellation URL if the shopper cancels their checkout on the Amazon Pay hosted page.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `placement`        | <p>The location where you placed the Amazon Pay button on your website. Your options are <code>Home</code>, <code>Cart</code>, <code>Product</code>, <code>Checkout</code>, or <code>Other</code>.<br><strong>Note</strong>: If you place the Amazon Pay button on the <code>Checkout</code> page, it is a standard checkout. If you place it on <code>Home</code>, <code>Cart</code>, <code>Product</code>, or <code>Other</code> page, it is an express checkout.</p>                                                                                                                                                                                |
| `checkoutLanguage` | The language used on the checkout page. Your options are `en_US`, `en_GB`, `de_DE`, `fr_FR`, `it_IT`, `es_ES`, or `ja_JP`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

See [How it works](../../../supported-payment-methods/amazon-pay.md#how-it-works) for more information on Amazon Pay's Express Checkout flow.

## Step 2: Use the authorized source

### Option 1. Attach the source to a cart

Once the shopper signs in to Amazon and authorizes the [source](../../../../general-resources/reference/elements/amazon-pay-element.md#source), you can [attach the source to a cart](../../../sources/using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).&#x20;

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Option 2. Attach the source to a shopper

Once the shopper signs in to Amazon and authorizes the [source](../../../../general-resources/reference/elements/amazon-pay-element.md#source) for a subscription, you can [attach the source for the customer](../../../sources/#attaching-a-payment-method-to-a-customer-or-payment-option).&#x20;

{% tabs %}
{% tab title="POST /v1/shoppers/me/payment-options" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Token",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
