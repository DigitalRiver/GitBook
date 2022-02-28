---
description: Learn how to configure the Payment and Billing Address subflow.
---

# Configure the Payment and Billing Address subflow

You need to configure the payment subflow to add My Wall and Digital River payment support. To configure the Payment and Billing Address subflow:

1. Click **Setup** ![](../../../../.gitbook/assets/Setup.png).
2. Type `Flows` in the **Quick Find** field and click **Flows**. \
   ![](<../../../../.gitbook/assets/Quick Find - Flows.png>)
3. Scroll down and click **Subflow - Payment and Billing Address**. The Flow Builder opens in a separate tab.\
   ![](<../../../../.gitbook/assets/Flows - Subflow - Checkout Summary.png>)&#x20;
4. Drag the **Screen** element from the left pane and drop it in the right pane.
5. Type `placeOrderConfirmation` in the **Label** field on the **Edit Screen** dialog.![](<../../../../.gitbook/assets/Edit-screen - placeOrderConfirmation (1).png>)&#x20;
6. Type `drb2b_paymentDetails` in the **Search Components** field and click **drb2b\_paymentDetails**.\
   ![](<../../../../.gitbook/assets/Search components - drb2b\_paymentDetails (1).png>)
7. Drag **drb2b\_paymentDetails** to where you want it to appear on the Edit Screen.\
   ![](<../../../../.gitbook/assets/Edit Screen - drb2b\_paymentDetails.png>)
8. Enter the following values in the fields:
   * **API Name**: Type `paymentDetails` or any other name with no restrictions.
   * **Cart Id**: Type `{!cartId}`.\
     ![](../../../../.gitbook/assets/brb2b\_paymentDetails.png)
9. Type `drb2b_orderSummary` in the **Search components** field and click **drb2b\_orderSummary**. \
   ![](<../../../../.gitbook/assets/Search components drb2b\_OrderSummary.png>)
10. Drag **drb2b\_orderSummary** to where you want it to appear on the Edit Screen.![](<../../../../.gitbook/assets/Edit Screen - drb2b\_orderSummary.png>)
11. Enter the following values in the fields:
    * **API Name**: Type `orderSummary` or any other name with no restrictions.
    * **ByPass Validation**: Type `{!$GlobalConstant.False}` or `{!$GlobalConstant.True}` (default value).\
      **Note**: Set the value to `{!$GlobalConstant.False}` whenever you want to use the `drb2b_drTermComponent` on the Place Order page. See [DR terms component](../../../../extend-the-salesforce-lightning-app/customizing-the-lightning-web-components/components/dr-terms-component.md) for more information.
    * **Record Id**: Type `{!cartId}`.
    * **Show All**:  Type `{!$GlobalConstant.True}`.
    * **Show Duty**: Type `{!$GlobalConstant.True}`.
    * **Show Grand Total**: Type `{!$GlobalConstant.True}`.
    * **Show IOR Tax**: Type `{!$GlobalConstant.True}`.
    * **Show Place Order**: Type `{!$GlobalConstant.True}`.
    * **Show Regulatory Fee**: Type `{!$GlobalConstant.True}`.
    * **Show Shipping**: Type `{!$GlobalConstant.True}`.
    * **Show Subtotal**: Type `{!$GlobalConstant.True}`.
    * **Show Tax**: Type `{!$GlobalConstant.True}`.\
      ![](../../../../.gitbook/assets/drb2b\_orderSummary.png)
12. Type `drb2b_drUtil` in the **Search components** field and click **drb2b\_drUtil** . ![](<../../../../.gitbook/assets/Search components drb2b\_drUtil.png>)
13. Drag **drb2b\_drUtil** to where you want it to appear on the Edit Screen.![](<../../../../.gitbook/assets/Edit Screen - drb2b\_drUtil.png>)
14. Type `drb2b_Util` or any other name with no restrictions in the **API Name** field.
15. Click **Done**.

{% hint style="info" %}
To continue editing the Payment and Billing Address subflow, see:

* [Edit the Payment Method screen](edit-the-payment-method-screen.md)
* [Edit the decision elements](edit-the-decision-elements.md)
* [Link the screen components](link-screen-components.md)
{% endhint %}
