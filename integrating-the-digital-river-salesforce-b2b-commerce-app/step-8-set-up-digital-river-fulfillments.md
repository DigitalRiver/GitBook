---
description: Learn how to set up Digital River fulfillments.
---

# Step 8: Set up Digital River fulfillments

When a cart is successfully submitted, an order is created in both Salesforce and Digital River. On the Digital River end, an order has a defined lifecycle with different stages. An event is created in Digital River when the order goes to a different stage in its lifecycle.

Whenever a Digital River Order is created, and the Payment has been authorized (passed fraud check), then the `order.accepted` event is created. This event triggers the fulfillment flow between Salesforce and Digital River. Currently, the Digital River App supports fulfillments at the line- item level except for cancellations which can be done at both the order and line-item level.

## Fulfillment flow <a href="#fulfillment-flow" id="fulfillment-flow"></a>

The following sequence diagram outlines the flow during fulfillment.

![](<../.gitbook/assets/Fulfillment\_Flow\_Phase-2.0 (1).png>)

The following list shows the sequence of steps in the fulfillment flow:

1. On successful Digital River order creation and payment authorization, an `order.accepted` event is created at the Digital River end.
   * This will send a notification to Salesforce by making a call to the following registered webhook endpoint exposed through the Digital River B2B App: `<>/services/apexrest/digitalriverv2/ DROFIOrderMgmNotification/`
   * This notification has all the relevant information like the type of event and the data associated with the event.
   * The app creates a Digital River fulfillment record in Salesforce with the Digital River order identifier. **OFI Received** flag on this record will be set to `TRUE`.
   * Clients should start their fulfillment process only after the OFI Received flag is checked on the Digital River fulfillment record for the order as this indicates that Digital River was able to authorize the payment and it has passed the fraud check.
2. Whenever a line item is fulfilled at the client-side, they need to update the Digital River Order Item State field on CC Order Item to **fulfilled**.
   * This will create a Digital River Line Item Fulfillment Record for this line item.
   * The Digital River Line Item Fulfillment Record will have all the relevant information like CC Order Item Id, Digital River Line Item ID, Line Item Quantity, Parent Digital River Fulfillment Record Id, and other information required to send fulfillment information to Digital River. Currently, the app does not support partial fulfillment.
   * **EFN OrderItem Status** field will be **Open** when this record is initially created.
   * The fulfillment job runs on a schedule and picks up all Digital River Line Item Fulfillment records whose **EFN OrderItem Status** is either **Open** or **Pending**.
     * EFN OrderItem Status will be set to `Pending` if there is a failure while sending fulfillment information to Digital River.
     * EFN OrderItem Status will be set to `Completed` when the fulfillment information is successfully sent to Digital River.
3. Digital River Order will be moved to `Completed` state, when fulfillment information is sent for all the line items in that order and funds are captured.
   * This will create an `order.complete` event at the Digital River end.
   * On creation of this event, a notification will be sent to the following registered webhook endpoint: `<>/services/apexrest/digitalriverv2/ DROrderCompleteNotification/`
   * The app sets the **OCN Received** flag on the Digital River Fulfillment record to `true`.
   * The **Digital River Order state** field on CC Order is updated to **complete**.

{% hint style="info" %}
**Note:** See [Step 8e Set up Webhooks for Fulfillment using Postman](step-8-set-up-digital-river-fulfillments.md#step-7e-set-up-webhooks-for-fulfillment-using-postman) for instructions on registering a Webhook URL.
{% endhint %}

## Cancellation flow between Salesforce and Digital River <a href="#cancellation-flow-between-salesforce-and-digital-river" id="cancellation-flow-between-salesforce-and-digital-river"></a>

You can request a cancellation at the order as well as at the line-item level. However, you can only cancel at the order level when none of the line items in the order are previously fulfilled. The following list explains the conditions when you can cancel a CC Order:

* The Digital River Order State on CC Order is `accepted` or `pending_payment` or `in_review` or `blocked.`
* The Digital River Order Item state on CC Order Items is either `created` or `cancelled.`

{% hint style="info" %}
If the above conditions are not satisfied, then an error will occur when trying to cancel the CC order.
{% endhint %}

## Order-level cancellation flow

The following list shows the sequence of steps between Salesforce and Digital River during an order-level cancellation:

1. Set the **Digital River Order State** field on CC Order to `cancelled`.
2. The CC Order Trigger in the Digital River App will update the **Digital River Order State** field on the Digital River Fulfillment record for this Order to `cancelled`.
3. The Order Level Fulfillment job runs on a schedule and picks up all Digital River fulfillment records whose **EFN Status** is `Open` or `Pending` and **Digital River Order State** is `cancelled`.
4. The Order Level Fulfillment job will take care of sending cancellation requests for all the line items in the order.
5. The **EFN Status** on the Digital River Fulfillment record will be updated to `Completed` once the cancellation information is successfully sent to Digital River.
6. The **OCN Received** flag on the Digital River Fulfillment record will not be updated to `true` for order-level cancellations.

## Line-item level cancellation flow <a href="#line-item-level-cancellation-flow" id="line-item-level-cancellation-flow"></a>

This flow is exactly similar to the steps mentioned in the [Fulfillment flow](step-8-set-up-digital-river-fulfillments.md#fulfillment-flow). The only difference is in Step 2 where you need to update the **Digital River Order Item State** field on the CC Order Item to `cancelled` instead of `fulfilled`. The remainder of the flow will remain the same.

{% hint style="info" %}
For order-level cancellation, you should only set the **Digital River Order State** field on CC Order to `cancelled`. The **Digital River Order Item State** field on **CC Order Items** should be set to `cancelled` only when you create a line-item level cancellation.
{% endhint %}

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

1. Create a new profile:
   * Click **Setup** ![](<../.gitbook/assets/setupicon (8) (5).png>) and select **Setup** from the dropdown list.
   * Under **Administration**, expand **Users**, and click **Profiles**. \
     ![](<../.gitbook/assets/Install DR B2B API Connector45.png>)
   * From the Profiles page, click **New** to create a new profile. ![](<../.gitbook/assets/Install DR B2B API Connector46.png>)
   * Select **Standard User** from the **Existing Profile** dropdown list. ![](<../.gitbook/assets/Install DR B2B API Connector47.png>)
   * Type `DRB2B Connector API User` in the **Profile Name** field. You're essentially cloning the Standard User profile to this new profile.
   * Click **Save**.
2. Set the password policy for this profile to never expire:
   * Under **Administration**, expand **Users**, and click **Profiles**.
   * Click the **DRB2B Connector API User** link under the **Name** column on the Profiles page.
   * Under **System** on the Profiles page, click the **Password Policies** link. ![](<../.gitbook/assets/Install DR B2B API Connector48.png>)
   * Click **Edit**.
   * Select **Never expires** from the **User passwords expire in** dropdown list. ![](<../.gitbook/assets/Install DR B2B API Connector49.jpg>)
   * Click **Save**.
3. Create a Fulfillment Integration User and assign the user to this profile.
   * Under **Administration**, expand **Users**, and click **Profiles**.
   * Click the **DRB2B Connector API User** link under the **Name** column on the Profiles page.
   * Click **Assigned Users**.
   * Click **New User**.
   * Assign a Fulfillment Integration User to this profile, complete the required fields, and click **Save**.

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

## Step 8e: Set up webhooks for fulfillment using Postman <a href="#step-7e-set-up-webhooks-for-fulfillment-using-postman" id="step-7e-set-up-webhooks-for-fulfillment-using-postman"></a>

Digital River uses webhooks to notify the app when events occur. As part of the fulfillment process, the app looks for two events: `order.accepted` and `order.complete`.

The `order.accepted` event occurs whenever a Digital River order is submitted, and the payment is **Authorized** (funds are not captured yet).

The `order.complete` event occurs whenever an order is both fulfilled and captured (funds are captured).

Follow the steps below to register webhook URLs for your Digital River site so that Digital River can notify the app when the `order.accepted` and `order.complete` events occur.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

You will need the following information before you set up the webhook URLs.

* **Username** of Fulfillment Integration User.
* **Password** of Fulfillment Integration User.
* **Client Id** of Connected App **DigitalRiver B2B Fulfillment** created in [step 8a](step-8-set-up-digital-river-fulfillments.md#step-7a-create-a-connected-app).
* **Client Secret** of Connected App **DigitalRiver B2B Fulfillment** created in [step 8a](step-8-set-up-digital-river-fulfillments.md#step-7a-create-a-connected-app).
* **Security Token** of Fulfillment Integration User.

### Register the Webhook URL for the `order.accepted` event <a href="#register-the-webhook-url-for-the-order-accepted-event" id="register-the-webhook-url-for-the-order-accepted-event"></a>

1. Open Postman.
2. Set the HTTP method to **POST**.
3. Set the URL as https://api.digitalriver.com/webhooks.
4. Set the HTTP body as shown in the following example:

```
{
    "types": [
        "order.accepted"
    ],
    "address": "<<SF_My_Domain_Name>>/services/apexrest/digitalriverv2/DROFIOrderMgmNotification/",
    "apiVersion": "default",
    "enabled": true,
    "transportType": "OAUTH",
    "oauth": {
        "tokenEndPoint": "<<SF_OAuth_Access_Token_Endpoint>",
        "userName": "<<Fulfillment_User_SF_Username>>",
        "password": "<<Fulfillment_User_SF_Password+SecurityToken>>",
        "clientID": "<<Fulfillment_ConnectedApp_Client_Id>>",
        "clientSecret": "<<Fulfillment_ConnectedApp_Client_Secret>>",
        "grantType": "password"
    }
} 
```

{% hint style="info" %}
**Note:** The URL for the `tokenEndpoint`is “https://test.salesforce.com/services/oauth2/token” for the sandbox and “https://login.salesforce.com/services/oauth2/token” for production.
{% endhint %}

### Register the webhook URL for the `order.complete` event <a href="#register-the-webhook-url-for-the-order-complete-event" id="register-the-webhook-url-for-the-order-complete-event"></a>

1. Open Postman.
2. Set the HTTP method to **POST**.
3. Set the URL as https://api.digitalriver.com/webhooks.
4. Set the HTTP body as shown in the following example:

```

    "types": [
        "order.complete"
    ],
    "address": "<<SF_My_Domain_Name>>/services/apexrest/digitalriverv2/DROrderCompleteNotification/",
    "apiVersion": "default",
    "enabled": true,
    "transportType": "OAUTH",
    "oauth": {
        "tokenEndPoint": "<<SF_OAuth_Access_Token_Endpoint>",
        "userName": "<<Fulfillment_User_SF_Username>>",
        "password": "<<Fulfillment_User_SF_Password+SecurityToken>>",
        "clientID": "<<Fulfillment_ConnectedApp_Client_Id>>",
        "clientSecret": "<<Fulfillment_ConnectedApp_Client_Secret>>",
        "grantType": "password"
    }
} 
```

A successful request returns a 200 OK response. Once configured, you can see these [webhooks](https://docs.digitalriver.com/digital-river-api/dashboard/developers/webhooks) in the [Digital River Dashboard](https://dashboard.digitalriver.com).

![](<../.gitbook/assets/Install DR B2B API Connector53.jpg>)

​
