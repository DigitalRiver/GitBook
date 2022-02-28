---
description: Learn how to create a new sharing set.
---

# Step 7: Create a new sharing set

Create a new sharing set in Community Settings to grant update access to the custom `taxExemptId` field in the Account object and update the sharing settings.

## Step 7a: Create a new sharing set <a href="#step-7a-create-a-new-sharing-set" id="step-7a-create-a-new-sharing-set"></a>

To create a new sharing set:

1. Click **Setup** ![](../.gitbook/assets/Setup.png) and select **Setup** from the dropdown list.
2. Type `communities settings` in the **Quick Find** field and press **Enter**. ![](../.gitbook/assets/Search-for-communities-settings.png)
3. Click **Communities Settings**. \
   ![](../.gitbook/assets/Communities-Settings.png)
4. Scroll down to **Sharing Sets** and click **New**. The New Sharing Set page appears.
5. Type `Account Sharing – VAT` in the **Label** field.
6. Type `Account_Sharing_VAT` in the **Sharing Name** field.
7. Type `Sharing of Account Field for VAT` in the **Description** field.
8. From **Available Profiles**, select your Storefront Community profiles used by the Salesforce Admin users and click **Add** to move it to **Selected Profiles**.
9. From **Available Objects**, select **Account** and click **Add** to move it to **Selected Objects**.
10. Click the **Set Up** link under **Configure Access**. The Access Mapping for Account dialog appears.
11. Select **Account** from the **User** dropdown list.
12. Select **Id** from the **Target Account** dropdown list.
13. Select **Read/Write** from the **Access level** dropdown list. \
    ![](../.gitbook/assets/API-enabled-oauth-settings.png)
14. Click **Update**. The New Sharing Set page displays should look like: \
    ![](../.gitbook/assets/New-Sharing-Set.png)
15. Click **Save**.

## Step 7b. Update the sharing settings for your organization <a href="#step-7b-update-the-sharing-settings-for-your-organization" id="step-7b-update-the-sharing-settings-for-your-organization"></a>

To update the sharing settings for your organization:

1. Click **Setup** ![](../.gitbook/assets/Setup.png) and select **Setup** from the dropdown list.
2. Type `sharing settings` in the **Quick Find** field and press **Enter**. \
   ![](../.gitbook/assets/Search-for-sharing-settings.png)
3. Click **Sharing Settings**. The Sharing Setting page appears.
4. Select **CC Order** from the **Manage Settings for** dropdown list.
5. Click **Edit**. The Organization-Wide Sharing Defaults Edit page appears.
6. Scroll down to **CC Invoice** and select **Public Read/Write** from the **Default Internal Access** dropdown list. \
   ![](../.gitbook/assets/CC-Invoice.png)
7. Scroll down to **CC Order** and select **Public Read/Write** from the **Default Internal Access** dropdown list. \
   ![](../.gitbook/assets/CC-Order.png) \
   Scroll down to **CC Transaction** and select **Public Read Only** from the **Default Internal Access** dropdown list. \
   ![](../.gitbook/assets/CC-Transaction-Payment.png)
8. Scroll down and click **Save**.
