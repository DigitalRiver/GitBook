---
description: Learn more about the checkout process.
---

# Order checkout

Once the products are added to the cart and the shopper proceeds to checkout, the shopper has to fill in the billing and shipping information on the **Checkout** page. Shoppers need to click **Calculate Total** to see the product total and payment methods and every time the shopper changes anything in **Address**, **Name**, or any other field, they will have to click **Calculate Total** to see the changes.

You can find the button below the **Tax Exemption** section.

![](<../.gitbook/assets/Checkout-page (6).png>)

![](<../.gitbook/assets/Calculate-Total-button (1).png>)

On the **Checkout** page, the shopper can opt for tax exemption based on the address they provided in the **Tax Exemption** section.

If the address country is the United States, the shopper will be prompted to upload their certificate.

Once the shopper places the order, the tax certificate is sent to Digital River for manual verification. Based on the results of the verification, the shopper will be notified whether or not their tax exemption certificate is valid.&#x20;

![](<../.gitbook/assets/Tax-Exemption (1).png>)

If the address country is other than the United States, it will ask the shopper to enter the VAT number. An API call will be made to the Digital River platform to verify the VAT number. Upon successful verification, the tax will be exempted for current and future purchases.

![](<../.gitbook/assets/Tax-Exemptions-for-Other-Countries (2).png>)

The payment options that appear on the **Checkout** page are based on the payment methods configured for your account within the Digital River Drop-in.&#x20;

![](<../.gitbook/assets/Payment-Options (2).png>)

Clicking **Your Saved Payment Methods** will show all the saved payment methods.&#x20;

![](<../.gitbook/assets/Saved-Payment-Methods (1).png>)

To select a payment method, click **Authenticate and Select**. The payment method will appear as the selected payment method.

![](<../.gitbook/assets/Selected-Payment-Method (4).png>)

To add a new payment method to the available payment methods, click **Add new payment method**, select a payment method, and then click **Place Order**.&#x20;

The Store Manager or Admin view orders by going to **WooCommerce** and click **Orders**. By default, the order status will be **Pending** when the order is placed. Once the order passes the fraud management system, the status will change to **Ready to fulfill**.

### Order Management Flow

The following process shows the order management flow between Digital River and WooCommerce.

1. When a shopper places an order, the status changes to **Pending** by default until it passed the Digital River fraud system.
2. When the order status changes to **Accepted** in Digital River, the WooCommerce order status will change to **Ready to fulfill**.
3. Optional: If the automatic order fulfillment module is active, it will fulfill the order and change the status to **Fulfilled**.
4. When Digital River changes the status of the order to **Complete**, the status will change to **Completed** in WooCommerce.\


