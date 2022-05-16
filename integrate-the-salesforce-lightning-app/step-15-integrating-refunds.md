---
description: Learn how to integrate refunds.
---

# Step 15: Integrating refunds

You can manage refunds at the order and line-item level from the Digital River [Dashboard](https://dashboard.digitalriver.com). The Salesforce Lightning app provides a Refunds button on the order. When you click the **Refunds** button, you will be redirected to the Order details page in the Dashboard.

{% hint style="info" %}
The Refunds button is only available to users assigned to the [DigitalRiver Connector - Refunds permission set](step-13-manage-permission-sets.md).
{% endhint %}

To add the Refunds button to your Order layout:

1. Click the App Launcher ![](<../.gitbook/assets/App launcher.png>).
2. Type `Orders` in the **Search** field and click **Orders**.\
   ![](../.gitbook/assets/Orders.png)
3. Click a link under the **Order Number** column.\
   ![](<../.gitbook/assets/Orders Recently Viewed.png>)
4. Click **Setup** ![](<../.gitbook/assets/Setup (1).png>) and select **Edit Page**.\
   ![](<../.gitbook/assets/Setup Edit Page.png>)
5. Click the top panel.\
   ![](<../.gitbook/assets/Top panel - No Refund button.png>)
6. Click **Upgrade Now** button on the panel to the right of the Lightning App Builder.![](<../.gitbook/assets/Upgrade Now.png>)
7. Click **Migrate** from the **Dynamic Actions** dialog and then click **Next**.\
   ![](../.gitbook/assets/Migrate.png)
8. Select **Order Layout** and click **Finish**.
9. Click **Add Action** in the panel to the right.\
   ![](<../.gitbook/assets/Add Action.png>)
10. Type `Refunds` in the **Search actions** field and click **Refunds**.![](<../.gitbook/assets/Acions - Refunds.png>)
11. Click **+ Add Filter** to set the action visibility.\
    ![](<../.gitbook/assets/Add Filter.png>)
12. Clicked the **Advanced** tab and then click the **Select** button.\
    ![](<../.gitbook/assets/Add Filter - Select.png>)
13. Select **Permissions** from the filter list in the **Select field** dialog.![](<../.gitbook/assets/Select field.png>)
14. Select **Custom Permission** from the next filter list.\
    ![](<../.gitbook/assets/Select field - Custom Permission.png>)
15. Select **digitalriverv3.Enable\_Refunds\_Button** from the next filter list.![](<../.gitbook/assets/Select field - Enable Refunds Button.png>)
16. Click **Done**.
17. Set the **Value** field to **True** and click **Done**.\
    ![](<../.gitbook/assets/Set value to True.png>)
18. Click **Done**.\
    ![](<../.gitbook/assets/Click Done.png>)\
    The Refunds button appears in the top panel.\
    ![](<../.gitbook/assets/Top panel.png>)
19. Click **Save** and then click **Activate**.
