---
description: Learn how to configure the delivery method subflow.
---

# Configure the delivery method subflow

Customize this subflow by adding the `drb2b_drUtil` custom component. This component communicates with the Address Detail component and display the Bill To and Ship To addresses on this screen.

To configure the Delivery Method subflow:

1. Click **Setup** ![](../../../.gitbook/assets/Setup.png).
2. Type `Flows` in the **Quick Find** field and click **Flows**. \
   ![](<../../../.gitbook/assets/Quick Find - Flows.png>)
3. Scroll down and click **Subflow - Delivery Method**. The Flow Builder opens in a separate tab.\
   ![](<../../../.gitbook/assets/Delivery method subflow 1.png>)&#x20;
4. Double-click the **Delivery Method** screen. \
   ![](<../../../.gitbook/assets/Subflow - Delivery Method.png>)&#x20;
5. Type `drb2b_drUtil` in the **Search components** field and click **drb2b\_drUtil**.\
   ![](<../../../.gitbook/assets/Search drb2b\_drUtil.png>)
6. Drag the **drb2b\_drUtil** pane to where you want it to appear on the Edit Screen. \
   ![](<../../../.gitbook/assets/Edit Screen drb2b\_drUtil Deliver Method.png>)
7. Type the API name (`drb2b_Util` or any other name with no restrictions) in the **API Name** field.\
   ![](<../../../.gitbook/assets/Edit Screen API Name drb2b\_Util.png>)
8. Click **Done**.
9. Click **Save As**. \
   ![](<../../../.gitbook/assets/Subflow - Delivery Method.png>)&#x20;
10. Enter the name of the delivery method subflow in the **Flow Label** field (for example, `DR Delivery Method`) and click **Save**.\
    ![](<../../../.gitbook/assets/Save as new flow Delivery Method.png>)
11. Click **Activate**. \
    ![](<../../../.gitbook/assets/Delivery method subflow 5.png>)&#x20;
