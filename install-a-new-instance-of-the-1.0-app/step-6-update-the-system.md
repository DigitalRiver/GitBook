---
description: Learn how to update the system.
---

# Step 6: Update the system

After you rebuild the system, you may need to perform full initialization through the Hybris Administration Console (HAC) if this is the first Hybris installation.&#x20;

If you have already performed full initialization, update your Hybris system as follows:&#x20;

1. From your web browser, select **HAC**, select **Platform**, and then click **Update**.
2. Select the following checkboxes under **General Settings**:
   * Update running system
   * Create essential data
   * Localize types\
     ![](<../.gitbook/assets/General settings (2).png>) \

3. Select the `digitalriveraddon`, `digitalriverbackoffice`, `digitalriverservices` **** checkboxes further down under **Project data settings**. \
   ![](<../.gitbook/assets/digitalriver backoffice (1).png>)\
   &#x20;![](<../.gitbook/assets/digitalriverservices and digitalriveraddon (1).png>)&#x20;
4. Click the **Update** button to update the Hybris system. This process can take up to three hours to complete.&#x20;
5. Verify the content in **Backoffice** by selecting **System**, then select **Business process**, select **Dynamic Processes Definitions**, select`order-process/return-process` and check the content.
6. After you finish updating the system,  if the changes do not appear in **Backoffice**, run the `projectdata-dynamic-business-process-order.impex` and `projectdata-dynamic-business-process-return.impex` files.



