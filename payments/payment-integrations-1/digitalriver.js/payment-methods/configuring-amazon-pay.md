---
description: Learn how to configure Amazon Pay for DigitalRiver.js with Elements.
---

# Configuring Amazon Pay

If you're using [DigitalRiver.js with Elements](../), you can create an [Amazon Pay](../../../supported-payment-methods/amazon-pay.md) payment method for your app or website in two easy steps:

* [Step 1: Create an Amazon Pay source using DigitalRiver.js](configuring-amazon-pay.md#create-a-google-pay-element)
* [Step 2: Use the authorized source](configuring-amazon-pay.md#step-2-use-the-authorized-source)

## Step 1: Create an AmazonPay source using Digital River.js

Amazon Pay is different from other payment methods. The shopper's payment information is pulled into the checkout directly from their Amazon Pay account.

To create an Amazon Pay source, follow the instructions in the [DigitalRiver.js reference guide](../reference/). If the shopper is paying for a subscription, you must [provide the `mandate.terms`](../../../../integration-options/checkouts/building-you-workflows/#elements) that the customer agreed to on your storefront [and set `autoRenewal` to `true`](broken-reference), and [`futureUse` to `true`](broken-reference).

### Create an Amazon Pay element

After setting up your library per the [DigitalRiver.js reference guide](../quick-start.md), [create an Amazon Pay element](../../../../developer-resources/reference/elements/amazon-pay-element.md#creating-an-amazon-pay-element) with any customizations you would like to apply.&#x20;

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
        },
    amazonPay: {
        //Amazon Pay will redirect to this URL after the buyer signs in
        returnUrl: '<return.com URL>', 
        //where the shopper will be returned after authorizing at Amazon Pay 
        resultReturnUrl: '<resultreturn.com URL>', 
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

| Attribute          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `country`          | An optional string that represents an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code. This is required when your session does not contain a shopper country.                                                                                                                                                                                                                                                                     |
| `returnUrl`        | The return URL redirects users to the Order Summary or Order Confirmation page. The shopper will be redirected to your Order Summary or Order Confirmation page after the shopper signs in to Amazon Pay and selects and confirms payment.                                                                                                                                                                                                                              |
| `resultReturnUrl`  | <p>A redirect to your Thank You page.</p><p>After Amazon Pay processes the payment, the shopper is redirected to your Thank You page. </p>                                                                                                                                                                                                                                                                                                                              |
| `cancelUrl`        | <p>A redirect from the cancelled login page to a page specified by you.<br>Amazon will redirect the shopper to this cancellation URL if the shopper cancels their checkout on the Amazon Pay hosted page.</p>                                                                                                                                                                                                                                                           |
| `placement`        | <p>The location where you placed the Amazon Pay button on your website. Your options are <code>Home</code>, <code>Cart</code>, <code>Product</code>, <code>Checkout</code>, or <code>Other</code>.<br><strong>Note</strong>: If you place the Amazon Pay button on the <code>Checkout</code> page, it is a standard checkout. If you place it on <code>Home</code>, <code>Cart</code>, <code>Product</code>, or <code>Other</code> page, it is an express checkout.</p> |
| `checkoutLanguage` | The language used on the checkout page. Your options are `en_US`, `en_GB`, `de_DE`, `fr_FR`, `it_IT`, `es_ES`, or `ja_JP`.                                                                                                                                                                                                                                                                                                                                              |

See [How it works](../../../supported-payment-methods/amazon-pay.md#how-it-works) for more information on Amazon Pay's Express Checkout flow.

## Step 2: Use the authorized source

### Option 1. Attach the source to a cart

Once the shopper signs in to Amazon and authorizes the [source](../../../../developer-resources/reference/elements/amazon-pay-element.md#source), you can [attach the source to the checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).&#x20;

{% tabs %}
{% tab title="POST /checkouts/{id}" %}
{% code overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Option 2. Attach the source to a customer

Once the shopper signs in to Amazon and authorizes the [source](../../../../developer-resources/reference/elements/amazon-pay-element.md#source) for a subscription, you can [save the source for the customer](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).&#x20;

{% tabs %}
{% tab title="POST /customers/{id}/sources/{sourcesId}" %}
{% code overflow="wrap" %}
```javascript
{
  "id": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
