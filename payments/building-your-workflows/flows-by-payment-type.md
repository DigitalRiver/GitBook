---
description: Understand the flows by payment type.
---

# Flows by payment type

Each payment method must follow a specific payment flow to ensure a seamless payment process. The payment flows and corresponding payment methods outlined below follow Digital River's recommended best practices.

## Standard payment flow

Use the following flow for standard payments: [Apple Pay](../supported-payment-methods/apple-pay.md), [credit cards](../supported-payment-methods/credit-cards.md), and [Google Pay](../supported-payment-methods/google-pay.md).&#x20;

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply the shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post).&#x20;
3. [Create a source using DigitalRiver.js](../payments-solutions/digitalriver.js/payment-methods/konbini.md#step-2-create-a-konbini-source-using-digitalriver.js). The source `state` is `chargeable`.
4. [Attach the source to the cart](flows-by-payment-type.md#attaching-multiple-payment-sources-to-the-cart).
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

## Delayed payment flow

### Submit a Konbini payment flow

Use the following flow for delayed payments, such as [Konbini](../supported-payment-methods/konbini.md).&#x20;

1. Get the store details.
2. [Create a source using DigitalRiver.js](../payments-solutions/digitalriver.js/payment-methods/konbini.md#step-2-create-a-konbini-source-using-digitalriver.js). The source `state` is `pending_funds`.
3. The customer transfers the funds to the Konbini payment provider.
4. The source `state` changes to `chargeable` when the funds are received.
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Submit a Boleto payment flow

To use [Boleto ](../supported-payment-methods/boleto.md)as a payment method:&#x20;

1. [Create a cart](../../shopper-apis/cart/creating-or-updating-a-cart/).
2. Optional. Set the locale and currency.\
   \
   `curl --location --request GET 'https://{host}/v1/shoppers/me.json? locale=pt_BR&currency=BRL' --header 'Content-Type: application/json'--header 'authorization: bearer ***\`
3. Optional. Set the cart address to the `BR` address.
4. [Attach the tax ID to the cart](broken-reference). The action inserts the tax ID into the payment session.
5. [Create a source using DigitalRiver.js](../payments-solutions/digitalriver.js/payment-methods/wire-transfer.md#step-2-create-a-wire-transfer-source-using-digitalriver.js) with a payment session ID. Note that the tax ID is required when creating the Boleto source. The payment session ID provides the tax ID.
6. [Attach the source to the cart](flows-by-payment-type.md#attaching-multiple-payment-sources-to-the-cart).
7. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Submit a Wire Transfer payment flow

Use the following flow for delayed payments, such as [Wire Transfer](../supported-payment-methods/wire-transfer.md).&#x20;

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply the shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post).&#x20;
3. [Create a source using DigitalRiver.js](../payments-solutions/digitalriver.js/payment-methods/wire-transfer.md#step-2-create-a-wire-transfer-source-using-digitalriver.js). The source `state` is `chargeable`.
4. [Attach the source to the cart](flows-by-payment-type.md#attaching-multiple-payment-sources-to-the-cart).
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).
6. The shopper receives the payment details and completes the payment. After the shopper finalizes the payment, the updated order status will appear in [Global Commerce](https://gc.digitalriver.com/gc/ent/home.do).

## Redirect then submit (RTS) payment flow

Use the following flow for RTS payment methods, such as [PayPal](../supported-payment-methods/paypal.md), [PayPal Billing Agreement](../supported-payment-methods/paypal-billing-agreement.md), [PayPal Credit](../supported-payment-methods/paypal-credit.md), [PayPal Pay in 3](../supported-payment-methods/paypal-pay-in-3.md), [PayPal Pay in 4](../supported-payment-methods/paypal-pay-in-4.md), and  [PayPal RatenZahlung (Installment Payment)](../supported-payment-methods/paypal-ratenzahlung-installment-payment.md)

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply the shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post).&#x20;
3. [Create a source using DigitalRiver.js](../../general-resources/reference/digitalriver-object.md#creating-sources). The source `state` is `pending_redirect`.
4. [Complete the redirect authorization](../../shopper-apis/cart/redirecting-to-a-digital-river-hosted-cart.md).
5. [Attach the source to the cart](flows-by-payment-type.md#attaching-multiple-payment-sources-to-the-cart). The session `state` is `requires_confirmation`.
6. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

## Submit then redirect (STR) payment flow

Use the STR payment flow for [Afterpay](../supported-payment-methods/afterpay.md), [Alipay (domestic)](../supported-payment-methods/alipay-domestic.md), [Alipay+ (cross-border)](../supported-payment-methods/alipay+-cross-border.md), [Amazon Pay Express Checkout](../supported-payment-methods/amazon-pay.md), [Bancontact](../supported-payment-methods/bancontact.md), [BLIK](../supported-payment-methods/blik.md), [CCAvenue](broken-reference), [Clearpay](../supported-payment-methods/clearpay.md), [iDEAL](../supported-payment-methods/ideal.md), [Klarna Financing](../supported-payment-methods/klarna.md), [Klarna Pay in 3](../supported-payment-methods/klarna.md), [Klarna Pay in 4](../supported-payment-methods/klarna.md), [Klarna Pay in 30 days](../supported-payment-methods/klarna.md), [Online Banking (IBP)](../supported-payment-methods/online-banking-ibp.md), [Online Banking (FPX)](../supported-payment-methods/fpx-online-banking.md), [Online Banking (Korea Bank Transfer)](../supported-payment-methods/korea-bank-transfer-online-banking.md), [PayCo](../supported-payment-methods/payco.md), [SEPA Direct Debit](../supported-payment-methods/sepa-direct-debit.md), and [TreviPay](../supported-payment-methods/trevipay.md), and [Trustly](../supported-payment-methods/trustly.md).&#x20;

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply the shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post).&#x20;
3. [Create a source using DigitalRiver.js with a session identifier (paymentSessionId)](../payments-solutions/digitalriver.js/payment-methods/configuring-trustly.md#step-2-create-a-trustly-source-using-digitalriver.js). The source state is `pending_redirect`.
4. [Attach the source to the cart](flows-by-payment-type.md#attaching-multiple-payment-sources-to-the-cart). The session `state` is `requires_confirmation`.
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/). The session `state` is `pending_redirect`.
6. Complete redirect authorization. The session `state` is `chargeable`.
7. [Resume cart](broken-reference) to complete post-order processing.

## Express checkout payment flow

Use the express checkout payment flow for [Amazon Pay Express Checkout](../supported-payment-methods/amazon-pay.md).

#### Submit an Amazon Pay flow

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
6. The shopper gets a second redirect to the Amazon Pay - Spinning page or Multi-factor Authentication (MFA) page. (Amazon Pay determines if the transaction requires MFA). The order will be in a [`source_pending_redirect`](../sources/#synchronous-or-asynchronous) state. You can [get an order by its identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders) to check the state of the order.
7. Optional. When you [resume the cart](../../shopper-apis/cart/resuming-cart-submission.md), the order will be in an [`accepted` state](broken-reference). &#x20;

{% tabs %}
{% tab title="GET /orders/{189917880336}" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/189917880336' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active/resume-cart' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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
