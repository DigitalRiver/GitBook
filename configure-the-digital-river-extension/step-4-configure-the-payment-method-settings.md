---
description: Learn how to configure the payment method settings.
---

# Step 4: Configure the payment method settings

Since Digital River acts as the merchant of record on all transactions, payment methods must be configured by Digital River. Work with your Digital River representative to configure the selection and display of payment methods in the Digital River Drop-in payment integration. Enabling Digital River payment methods and other payment methods on the configuration page for the same store will result in failures.

1. From the **Magento Admin panel**, select **Stores**, select **Conﬁguration**, select **Sales**, select **Payment Methods**.
2. In **Payment Methods**, make the following selections:
   * Select **Check/Money Order**. Then set **Enabled** to **No**.
   * Select **Cash On Delivery Payment**. Then set **Enabled** to **No**.
   * Select **Bank Transfer Payment**. Then set **Enabled** to **No**.
   * Select **Purchase Order**. Then set **Enabled** to **No**. Note that the Digital River 2.3.0 extension release now supports the [Purchase Order ](enabling-magentos-purchase-order-payment-method.md)payment method.&#x20;
   * Select **Digital River Payment**. Then set **Enabled** to **Yes**. Note that you can change the title. The recommended title is "Payment Options".
