---
description: Learn how to configure the payment method settings.
---

# Step 4: Configure the payment method settings

Since Digital River acts as the merchant of record on all transactions, payment methods must be configured by Digital River. Work with your Digital River representative to configure the selection and display of payment methods in the Digital River Drop-in payment integration. Enabling Digital River payment methods and other payment methods on the configuration page for the same store will result in failures.

1. From the **Magento Admin panel**, select **Stores**, select **Conﬁguration**, select **Sales**, select **Payment Methods**.
2. In **Payment Methods**, make the following selections:
   * Select **Zero Subtotal Checkout** if you want to allow orders to use 100% store credit or gift cards.\
     ![](../.gitbook/assets/Zero-Subtotal-Checkout.png)
   * Select **Check/Money Order**. Then set **Enabled** to **No**.\
     ![](../.gitbook/assets/Check-Money-Order.png)
   * Select **Bank Transfer Payment**. Then set **Enabled** to **No**.![](../.gitbook/assets/Bank-Transfer-Payment.png)
   * Select **Cash On Delivery Payment**. Then set **Enabled** to **No**.![](../.gitbook/assets/Cash-on-Delivery-Payment.png)
   * Select **Purchase Order**. Then set **Enabled** to **No**. Note that the Digital River 2.3.0 extension release now supports the [Purchase Order ](enabling-magentos-purchase-order-payment-method.md)payment method. ![](../.gitbook/assets/Purchase-Order.png)
   * Select **Digital River Payment**. Then set **Enabled** to **Yes**. Note that you can change the title. We recommended typing `Payment Options` in the **Title** field.![](../.gitbook/assets/Digital-River-Payment.png)

### Understand redirects on the Payment page

You can improve a customer's shopping experience in cases when it is required to redirect them out of the checkout flow to complete their transaction.

This situation can occur when:

* Customers pay using a payment method that redirects them to their website
* PSD2 regulations require that a shopper answer a 3D Secure Challenge Question when paying with a credit card

To improve this experience, Digital River has added an option to allow you to select where in the checkout flow a redirect happens. See [Configure General Settings](step-2-configure-the-digital-river-admin-settings.md) for instructions on how to set the flow for redirect payment methods.

You can choose whether your shoppers see the challenge question when clicking the **Continue** button within the Digital River **Drop In from the Payment** page of the checkout OR when clicking the **Place Order** button on the **Order Confirmation** page of the checkout. Please work with your Digital River representative to change the location of the PSD2 challenge question.

{% hint style="info" %}
This change is not supported by the PayPal payment method.
{% endhint %}
