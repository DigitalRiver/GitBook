---
description: Learn how to configure the shipping address subflow.
---

# Configure the shipping address subflow

Use this subflow to capture buyer information such as Bill To, Ship To, and Email.

1. Click **Setup** ![](../../../../.gitbook/assets/Setup.png).
2. Type `Flows` in the **Quick Find** field and click **Flows**. \
   ![](<../../../../.gitbook/assets/Quick Find - Flows.png>)
3. Scroll down and click **Subflow - Shipping Address**. The Flow Builder opens in a separate tab.\
   ![](<../../../../.gitbook/assets/Flows - Subflow - Shipping Address.png>)&#x20;
4. Drag the **Action** element from the left pane and drop it in the right pane. ![](<../../../../.gitbook/assets/Action element.png>)\
   The New Action popup dialog appears.\
   ![](<../../../../.gitbook/assets/New Action.png>)
5. Select **Type** from the **Filter By** dropdown list and click **Apex Action**. \
   ![](<../../../../.gitbook/assets/Filter By.png>)
6. In the **Search Apex actions** field, type `digitalriverv3_DRB2B_ClearData`,  and click **digitalriverv3\_DRB2B\_ClearData**.
7.  Toggle **cartIdList** to **Include**, and enter the following values in the fields:

    * **Label:** Type `DR Clear Data` or any other name with no restrictions.
    * **API** **Name**: Type `DR_Clear_Data`.
    * **cartIdList**: Type `{!cartId}`.

    ![](<../../../../.gitbook/assets/New Action completed fields.png>)
8. Click **Done**.
9. Drag the **Apex Action DR Clear Data** to the right of **Screen Shipping Address Screen** as shown below. \
   ![](<../../../../.gitbook/assets/Apex Action DR Clear Data.png>)
10. Click the link between **Start Checkout Flow** and **Shipping Address Screen** and press the **Delete** key on your keyboard.\
    ![](<../../../../.gitbook/assets/Apex Action DR Clear Data delete link.png>)
11. Click the circle below **Start Checkout Flow** and drag it to **Apex Action DR Clear Data**.\
    ![](<../../../../.gitbook/assets/Link Start Checkout Flow to Apex Action.png>)
12. Click the circle below **Apex Action DR Clear Data** and drag it to **Shipping Address Screen**. \
    ![](<../../../../.gitbook/assets/Link Apex Action DR Clear Data to Screen Shipping Address Screen.png>)
