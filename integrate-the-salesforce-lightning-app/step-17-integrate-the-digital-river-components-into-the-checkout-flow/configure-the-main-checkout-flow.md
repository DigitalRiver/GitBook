---
description: Learn how to configure the main checkout flow.
---

# Configure the main checkout flow

To configure the main checkout flow:

1. Click **Setup** ![](../../.gitbook/assets/Setup.png).
2. Type `Flows` in the **Quick Find** field and click **Flows**. \
   ![](<../../.gitbook/assets/Quick Find - Flows.png>)
3. Click **Checkout Flow Template**. The Flow Builder opens in a separate tab.\
   ![](<../../.gitbook/assets/Checkout Flow Template.png>)&#x20;
4. Create the subflow element for all the custom subflows (for example, the [DR Shipping Address](subflow-configuration/configure-the-shipping-address-subflow/), [DR Payment and Billing Address](subflow-configuration/configure-the-payment-and-billing-address-subflow/), [DR Checkout Summary](subflow-configuration/configure-the-checkout-summary-subflow.md), and [DR Delivery Method](subflow-configuration/configure-the-delivery-method-subflow.md)) created in the previous steps.
   1. Drag the **Subflow** element from the left panel to the right panel.
   2. Type the custom subflow name (for example, `DR Shipping Address`) in the **Reference Flow** field and click the item (for example, **DR Payment and Billing Address**) in the search results.
   3. Type the name of the subflow in the **Label** field (for example, **DR Payment and Billing Address**).\
      ![](<../../.gitbook/assets/New Subflow Label.png>)
   4. Type the appropriate value listed in the [subflow settings table](configure-the-main-checkout-flow.md#subflow-settings) for the custom subflow in each field. The following example shows the settings for the DR Payment and Billing Address subflow.\
      ![](<../../.gitbook/assets/New Subflow complete.png>)
   5. Under **Set Input Values**, toggle **cartId**, **currentState**, **nextState**, **orderId** (if applicable) to **Inlude**. Toggle **Saved\_Tax\_Identifier** (if applicable) to **Don't include**.\
      ![](<../../.gitbook/assets/New Subflow Set Input Values.png>)
5. Replace the OOTB flows with custom flows. &#x20;
   * **Shipping Address**: DR Shipping Address
   * **Delivery Method**: DR Delivery Method
   * **Checkout Summary**: DR Checkout Summary
   * **Payment and Billing Address**: DR Payment and Billing Address\
     ![](<../../.gitbook/assets/Replace OOTB flow with custom flow.png>)&#x20;
6. Click **Save As** and enter a name for the main checkout flow. \
   ![](<../../.gitbook/assets/Name for main checkout flow.png>)&#x20;
7. Click **Save**, then click **Activate**.

## Subflow settings

| Subflow                        | Settings                                                                                                                                                                                                                                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DR Shipping Address            | <p><strong>Cart Id</strong>: <code>{!cartId}</code><br><code></code><strong>Current state</strong>: {<code>!mainCheckoutSession.State}</code><br><strong>Next state</strong>: Inventory</p>                                                                                                 |
| DR Delivery Method             | <p><strong>Cart Id</strong>: <code>{!cartId}</code><br><code></code><strong><code>Current</code> state</strong>: {!<code>mainCheckoutSession.State}</code><br><strong>Next state</strong>: Taxes</p>                                                                                        |
| DR Checkout Summary            | <p><strong>Cart Id</strong>: <code>{!cartId}</code><br><code></code><strong>Current state</strong>: {!<code>mainCheckoutSession.State}</code><br><strong>Next state</strong>: Cart To Order<br><strong>Saved_Tax_Identifier</strong>: {!Saved_Tax_Identifier} </p>                          |
| DR Payment and Billing Address | <p><strong>Cart Id</strong>: <code>{!cartId}</code><br><code></code><strong>Current state</strong>: {!<code>mainCheckoutSession.State}</code><br><strong>Next state</strong>: Activate Order<br><strong>Order Id</strong>: <code>{!mainCheckout</code><br><code>Session.OrderId}</code></p> |
