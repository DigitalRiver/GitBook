---
description: Learn how to upgrade from previous version to version 1.1.
---

# Upgrading to version 1.1

Use the following instructions to upgrade from a previous version of the Digital River app for Salesforce Lightning to version 1.1. If you're installing a new version of this app, see [Install the Digital River app](integrate-the-salesforce-lightning-app/step-1-install-the-digital-river-app.md) for instructions.

1. Install the latest version of the Salesforce Lightning app as described in [Step 1](integrate-the-salesforce-lightning-app/step-1-install-the-digital-river-app.md).
2. Update the Shipping Address subflow described in [Configure the shipping address subflow](integrate-the-salesforce-lightning-app/step-17-integrate-the-digital-river-components-into-the-checkout-flow/subflow-configuration/configure-the-shipping-address-subflow/).\
   **Note**: We added some additional actions and components to this version of the app.
3. Update the Payments and Billing subflow described in [Configure the Payment and Billing Address subflow](integrate-the-salesforce-lightning-app/step-17-integrate-the-digital-river-components-into-the-checkout-flow/subflow-configuration/configure-the-payment-and-billing-address-subflow/) as follows:
   1. Remove the `Payment_Details` resource. Note that you can choose to leave it as is, but it will no longer be used.
   2. Add the `db2b_paymentDetails` component to the `placeOrder` screen.
4. [Enable the order.cancelled event](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/webhooks/creating-a-webhook#step-3-create-webhooks) from the Webhooks page on the [Digital River Dashboard](https://dashboard.digitalriver.com/login). See [Step 11](integrate-the-salesforce-lightning-app/step-11-set-up-webhooks.md) for complete instructions.\
   ![](<.gitbook/assets/enable order cancelled event.png>)
5. Add a new picklist value called `partially_cancelled` to the `DR_Order_Item_State__c` field on the `OrderItem` object.
6. Update the **Key** value for the **Connector Version** to `1.1/3.1` using the following instructions:
   1. Click **Setup** ![](<.gitbook/assets/Setup (1).png>) and select **Setup** from the dropdown list.
   2. Type `Custom Metadata Types` in the **Quick Find** field and then click **Custom Metadata Types**. The **Custom Metadata Types** page appears with the **All Metadata Types** list.
   3. Locate the **DR Connector Configuration** metadata type from the lists (Label) and click the **Manage Records** action next to that type selection. \
      ![](.gitbook/assets/CMDT\_list\_1.jpg)
   4. On the **DR Connector Configurations** page find the **Connector Version** setting (Label). Click **Edit** next to the **Connector Version** setting.\
      &#x20;![](.gitbook/assets/CMDT\_version\_2.jpg)
   5. Update the **Key** value for the **Connector Version** to `1.1/3.1` or as instructed by your project manager.\
      ![](.gitbook/assets/CMDT\_key\_3.jpg)
   6. Click **Save** after you have finished updating the version number and return to the **Home** page.\


