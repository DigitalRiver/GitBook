---
description: >-
  Amazon Pay is a global digital wallet paving the way for your brand to gain
  visibility and access to millions of existing Amazon customers.
---

# Amazon Pay

This payment method boasts a highly secure and seamless checkout experience, leveraging saved shipping and payment information in the shopper's Amazon account. As a result, the shopper can complete their transactions in 3 simple clicks and almost twice as fast as other payment options.

If you are interested in using Amazon Pay, contact your Customer Success Manager. The Customer Success Manager will send setup instructions for Amazon Pay after you sign the Amazon Pay addendum.

## How to configure&#x20;

How you configure Amazon Pay depends on whether you're using [DigitalRiver.js with Elements](../payments-solutions/digitalriver.js/) or[ Drop-in payments](../payments-solutions/drop-in/).

| DigitalRiver.js with Elements                                                                             | Drop-in payments |
| --------------------------------------------------------------------------------------------------------- | ---------------- |
| [Configuring Amazon Pay](../payments-solutions/digitalriver.js/payment-methods/configuring-amazon-pay.md) | Not supported    |

## How it works

Digital River supports Amazon Pay's Express Checkout flow.&#x20;

The shopper clicks the Amazon Pay Checkout button at checkout, and then they sign in to Amazon Pay to authorize payment and complete their purchase. &#x20;

Digital River accepts the shopper's billing and shipping addresses from the shopper's Amazon account and populates the checkout or order confirmation page with that information.&#x20;

{% hint style="success" %}
Amazon requires that you remove or hide the Edit buttons or links for the billing and shipping addresses on the order confirmation page because Amazon maintains that information. Digital River cannot update the billing and shipping information for an Amazon shopper. If needed, the shopper can also update the shipping and billing addresses from their Amazon account before completing actions on Amazon Pay.
{% endhint %}

### Amazon Pay Express Checkout flow

The following image shows Amazon Pay's Express Checkout flow for Commerce API.

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

The following Amazon Pay flow represents how your shoppers experience the payment process.

1. The shopper adds the product to the shopping cart
2. The shopper clicks the Shopping Cart
3. The shopper clicks the Amazon Pay button.
4. The shopper is redirected to Amazon Pay to sign in and select the shipping address (if required), and the payment method.
5. The shopper clicks the Submit button to place the order.&#x20;
6. The shopper gets a second redirect to Amazon Pay - Spinning page or Multi-factor Authentication (MFA) page. (Amazon Pay determines if the transaction requires MFA).

## Supported markets

For information on supported markets and currencies, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method/amazon-pay/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
