---
description: >-
  Amazon Pay is a global digital wallet paving the way for your brand to gain
  visibility and access to millions of existing Amazon customers.
---

# Amazon Pay

This payment method boasts a highly secure and seamless checkout experience, leveraging saved shipping and payment information in the shopper's Amazon account. As a result, the shopper can complete their transactions in 3 simple clicks and almost twice as fast as other payment options.

Contact your Customer Success Manager and sign an Amazon Pay addendum if you want to use Amazon Pay. The Customer Success Manager will send setup instructions for Amazon Pay.

## How to configure

How you configure Amazon Pay depends on whether you're using [DigitalRiver.js with Elements](../payment-integrations-1/digitalriver.js/) or [Drop-in payments](../payment-integrations-1/drop-in/).

| DigitalRiver.js with Elements                                                                                 | Drop-in payments |
| ------------------------------------------------------------------------------------------------------------- | ---------------- |
| [Configuring Amazon Pay](../payment-integrations-1/digitalriver.js/payment-methods/configuring-amazon-pay.md) | Not supported    |

## How it works

Digital River supports [Amazon Pay's Express Checkout flow](amazon-pay.md#amazon-pay-express-checkout-flow). Amazon Pay's Express Checkout uses an express checkout payment flow. The shopper clicks the Amazon Pay Checkout button at checkout, and then they sign in to Amazon Pay to authorize payment and complete their purchase. &#x20;

Digital River accepts the shopper's billing and shipping addresses from the shopper's Amazon account and populates the checkout or order confirmation page with that information.&#x20;

{% hint style="success" %}
Amazon requires that you remove or hide the Edit buttons or links for the billing and shipping addresses on the order confirmation page because Amazon maintains that information. Digital River cannot update an Amazon shopper's billing and shipping information. If needed, the shopper can also update their Amazon account's shipping and billing addresses before completing actions on Amazon Pay.
{% endhint %}

### Amazon Pay Express Checkout flow

The following image shows Amazon Pay's Express Checkout flow for Prebuilt Checkout.

{% file src="../../.gitbook/assets/Amazon Pay - DR API.png" %}
Amazon Pay Express Checkout flow
{% endfile %}

The following Amazon Pay flow represents how your shoppers experience the payment process.

1. The shopper adds the product to the shopping cart.
2. The shopper clicks the Amazon Pay button.
3. The shopper is redirected to Amazon Pay to sign in and select the shipping address (if required) and payment method.
4. The shopper signs in to Amazon Pay, selects a payment method such as a credit card, and provides their shipping address.
5. The shopper clicks the Submit button to place the order. \
   **Note**: You can [get an order by its identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders) to check the state of the order.
6. The shopper gets a second redirect to the Amazon Pay - Spinning page or Multi-factor Authentication (MFA) page. (Amazon Pay determines if the transaction requires MFA.) Based on the order state and session state, the shopper lands on the Thank You or Order Failed pages.

{% tabs %}
{% tab title="Step 5: GET /orders/{189917880336}" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/189917880336' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
    "id": "189917880336",
    ...
    "state": "pending_payment",
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Step 6: POST /orders/189917880336/refresh" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/orders/189917880336/refresh' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
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

## Supported markets

For information on supported markets and currencies, go to:

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method/amazon-pay/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
