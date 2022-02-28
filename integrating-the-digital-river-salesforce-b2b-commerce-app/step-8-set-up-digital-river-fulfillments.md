---
description: Learn how to set up Digital River fulfillments.
---

# Step 8: Set up Digital River fulfillments

## Enabling Digital River fulfillments

When you set up Digital River fulfillments, you will need to [create a profile](step-8-set-up-digital-river-fulfillments.md#step-7c-create-a-profile-and-fulfillment-integration-user) for a Fulfillment Integration User and [send the OAuth information for that user to Digital River](step-9-set-up-webhooks.md) to enable fulfillment.&#x20;

{% hint style="info" %}
Digital River must set up the Salesforce B2B Commerce App for Salesforce B2B Commerce under Manage Connected Apps before you can [set up OAuth](step-8-set-up-digital-river-fulfillments.md#step-7a-create-a-connected-app) for Digital River fulfillments.
{% endhint %}

See the [Appendix](../appendix/) for more information about:

* [Fulfillment flow](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MRazfhnbBY5nfyqbUlx/v/2.0/appendix/fulfillment-and-cancellation-flow#fulfillment-flow)
* [Cancellation flow](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MRazfhnbBY5nfyqbUlx/v/2.0/appendix/fulfillment-and-cancellation-flow#cancellation-flow-between-salesforce-and-digital-river)
* [Order-level cancellation flow](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MRazfhnbBY5nfyqbUlx/v/2.0/appendix/fulfillment-and-cancellation-flow#order-level-cancellation-flow)
* [Line-item cancellation flow](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MRazfhnbBY5nfyqbUlx/v/2.0/appendix/fulfillment-and-cancellation-flow#line-item-level-cancellation-flow)

## Step 8a: Create a connected app <a href="#step-7a-create-a-connected-app" id="step-7a-create-a-connected-app"></a>

To create a connected app for Digital River fulfillments, complete the following steps:

1. Sign in to Salesforce Org.
2. Click **Setup** ![](<../.gitbook/assets/setupicon (8) (4).png>) and select **Setup** from the dropdown list.
3. Type `app manager` in the **Quick Find** field and press **Enter**. \
   ![](<../.gitbook/assets/app\_mgr (1).png>)
4. Click **App Manager** in the search results.
5. Click **New Connected App**.
6. Under **Basic Information**, type `DigitalRiver B2B Fulfillment Connector` in the **Connected App Name** field. \
   ![](../.gitbook/assets/BasicInformation.png)
7. Provide your **API name** and your email address.
8. Select **Enable OAuth Settings**.
9. Under **API (Enable OAuth Settings)**, type `https://` in the **Callback URL** field. ![](<../.gitbook/assets/Install DR B2B API Connector39.png>)
10. Add **Access and manage your data (api)** to **Selected OAuth Scopes**. ![](<../.gitbook/assets/Install DR B2B API Connector40.png>)
11. Select the **Require Secret for Web Server Flow** check box.
12. Click **Save**. Allow 2-10 minutes for your changes to take effect on the server before using the connected app. \
    ![](<../.gitbook/assets/Install DR B2B API Connector41.jpg>)
13. Capture the **Client Id** and **Client Secret** information. They will be used while setting up webhooks for Fulfillment.

## Step 8b: Update Sharing Settings in Client Org <a href="#step-7b-update-sharing-settings-in-client-org" id="step-7b-update-sharing-settings-in-client-org"></a>

To update the Sharing Settings for the fulfillment flow, complete the following steps:

1. From **Setup**, enter `Sharing Settings` in the **Quick Find** field, and then select **Sharing Settings**.
2. Select **CC Order** from the **Manage sharing settings for** dropdown list.
3. Update the **Default Internal Access** to **Public Read/Write**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector42.jpg>)
4. Repeat steps 2-3 for the **CC Invoice** object. \
   ![](<../.gitbook/assets/Install DR B2B API Connector43.jpg>)
5. For the **CC Transaction Payment** object, you must select **Public Read Only** from the **Default Internal Access** dropdown list.&#x20;

![](<../.gitbook/assets/Install DR B2B API Connector44.jpg>)

## Step 8c: Create a profile and Fulfillment Integration User <a href="#step-7c-create-a-profile-and-fulfillment-integration-user" id="step-7c-create-a-profile-and-fulfillment-integration-user"></a>

To create a profile and assign it to a Fulfillment Integration User, complete the following steps:

### Create a new profile

1. Click **Setup** ![](<../.gitbook/assets/setupicon (8) (5).png>) and select **Setup** from the dropdown list.
2. Under **Administration**, expand **Users**, and click **Profiles**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector45.png>)
3. From the Profiles page, click **New** to create a new profile. ![](<../.gitbook/assets/Install DR B2B API Connector46.png>)
4. Select **Standard User** from the **Existing Profile** dropdown list. ![](<../.gitbook/assets/Install DR B2B API Connector47.png>)
5. Type `DRB2B Connector API User` in the **Profile Name** field. You're essentially cloning the Standard User profile to this new profile.
6. Click **Save**.

### Set the password policy for this profile to never expire

1. Under **Administration**, expand **Users**, and click **Profiles**.
2. Click the **DRB2B Connector API User** link under the **Name** column on the Profiles page.
3. Under **System** on the Profiles page, click the **Password Policies** link. ![](<../.gitbook/assets/Install DR B2B API Connector48.png>)
4. Click **Edit**.
5. Select **Never expires** from the **User passwords expire in** dropdown list. ![](<../.gitbook/assets/Install DR B2B API Connector49.jpg>)
6. Click **Save**.

### Create a Fulfillment Integration User and assign the user to this profile.

1. Under **Administration**, expand **Users**, and click **Profiles**.
2. Click the **DRB2B Connector API User** link under the **Name** column on the Profiles page.
3. Click **Assigned Users**.
4. Click **New User**.
5. Assign a Fulfillment Integration User to this profile, complete the required fields, and click **Save**.

![](<../.gitbook/assets/Install DR B2B API Connector50.jpg>)

## Step 8d: Assign the Fulfillment Integration User to Digital River Salesforce B2B Commerce Fulfillment Permission Set <a href="#step-7d-assign-the-fulfillment-integration-user-to-drb-2-b-fulfillment-permission-set" id="step-7d-assign-the-fulfillment-integration-user-to-drb-2-b-fulfillment-permission-set"></a>

To add the new user to the Digital River Salesforce B2B Commerce App permission set:

1. From Setup, enter `permission sets` in the **Quick Find** field and press **Enter**.
2. Click **Permission Sets**. The Permission Sets page appears.
3. Select the permission set **DRB2B Fulfillment Permission Set**.
4. Click **Manage Assignments**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector51.jpg>)
5. Click **Add Assignments** and add the **Fulfillment Integration** user **Digital River** created in [Step 8c Create a profile and Fulfillment Integration User](step-8-set-up-digital-river-fulfillments.md#step-7c-create-a-profile-and-fulfillment-integration-user) to the permission set.&#x20;

![](<../.gitbook/assets/Install DR B2B API Connector52.jpg>)
