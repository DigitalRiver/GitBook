---
description: >-
  Amazon Pay is a global digital wallet paving the way for your brand to gain
  visibility and access to millions of existing Amazon customers.
---

# Amazon Pay

This payment method boasts a highly secure and seamless checkout experience, leveraging saved shipping and payment information in the shopper's Amazon account. As a result, the shopper can complete their transactions in 3 simple clicks and almost twice as fast as other payment options.

Contact your Customer Success Manager and sign an Amazon Pay addendum if you want to use Amazon Pay. The Customer Success Manager will send setup instructions for Amazon Pay.

## How to configure&#x20;

How you configure Amazon Pay depends on whether you're using [DigitalRiver.js with Elements](../payments-solutions/digitalriver.js/) or[ Drop-in payments](../payments-solutions/drop-in/).

<table><thead><tr><th width="265">DigitalRiver.js with Elements</th><th>Drop-in payments</th></tr></thead><tbody><tr><td><a href="../payments-solutions/digitalriver.js/payment-methods/configuring-amazon-pay.md">Configuring Amazon Pay</a></td><td>Not supported</td></tr></tbody></table>

## How it works

Digital River supports [Amazon Pay's Express Checkout flow](../building-your-workflows/flows-by-payment-type.md#submit-an-amazon-pay-flow). Amazon Pay's Express Checkout uses an [express checkout payment flow](../building-your-workflows/flows-by-payment-type.md#express-checkout-payment-flow). The shopper clicks the Amazon Pay Checkout button at checkout, and then they sign in to Amazon Pay to authorize payment and complete their purchase. &#x20;

Digital River accepts the shopper's billing and shipping addresses from the shopper's Amazon account and populates the checkout or order confirmation page with that information.&#x20;

{% hint style="success" %}
Amazon requires that you remove or hide the Edit buttons or links for the billing and shipping addresses on the order confirmation page because Amazon maintains that information. Digital River cannot update an Amazon shopper's billing and shipping information. If needed, the shopper can also update their Amazon account's shipping and billing addresses before completing actions on Amazon Pay.
{% endhint %}

### Amazon Pay Express Checkout flow

The following image shows Amazon Pay's Express Checkout flow for Commerce API.

<div align="left">

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

</div>

The following Amazon Pay flow represents how your shoppers experience the payment process.

1. The shopper adds the product to the shopping cart
2. The shopper clicks the Shopping Cart
3. The shopper clicks the Amazon Pay button.
4. The shopper is redirected to Amazon Pay to sign in and select the shipping address (if required) and the payment method.
5. The shopper clicks the Submit button to place the order.&#x20;
6. The shopper gets a second redirect to the Amazon Pay - Spinning page or Multi-factor Authentication (MFA) page. (Amazon Pay determines if the transaction requires MFA).
7. Optional. When you [resume the cart](../../shopper-apis/cart/resuming-cart-submission.md), the order will be in an [`accepted` state](broken-reference). &#x20;

{% tabs %}
{% tab title="GET /orders/{189917880336}" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://api.digitalriver.com/orders/189917880336' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```javascript
{
    "id": "189917880336",
    ...
    "state": "source_pending_redirect",
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/resume-cart" %}
{% code overflow="wrap" %}
```javascript
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active/resume-cart' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```javascript
{
    "id": "189917880336",
    ...
    "state": "accepted",
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Supported markets

For information on supported markets and currencies, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method/amazon-pay/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
