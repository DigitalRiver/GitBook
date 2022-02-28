---
description: Learn how to configure the From email address for system generated email.
---

# Step 16: Configure the From email address

When sending an email, Salesforce usually puts the current user's email address as the sender's address. This is OOTB behavior. Your business may, however, require you to use an organization-wide email address (for example, support@acme.com) regardless of the user who actually sends the messages.

When defining an organization-wide email address, note the following:

* The [organization-wide email address](step-16-configure-the-from-email-address.md#setting-the-from-email-address-for-system-generated-email) must match the [email address for the system email specified in the Digital River app](step-16-configure-the-from-email-address.md#setting-the-from-email-address-in-the-digital-river-app). If they don't, the system assigns the email address of the user who applied the changes to as the From address, not the generic or role-based email address.
* The Digital River app allows you to configure the From email address for system email.

## Setting the From email address for system-generated email

To change the default From address for the system email and changed the OOTB behavior:

1. Click **Setup** ![](<../.gitbook/assets/Setup (1).png>) and select **Setup** from the dropdown list.\
   &#x20;![](<../.gitbook/assets/Page layout 1.png>)&#x20;
2. Type `Organization-Wide Addresses` in the **Quick Find** field and then click **Organization-Wide Addresses**.\
   ![](<../.gitbook/assets/Organization-Wide Addresses.png>)
3. Click **Add** next to **User Selectable Organization-Wide Email Addresses**.![](<../.gitbook/assets/Organization-Wide Addresses page (1).png>)
4. Type a name (for example, `Acme Support`) you want to associate with the email address in the **Display Name** field.
5. Type the email address (for example, `support@acme.com`) you want to use in the **Email Address** field.\
   ![](<../.gitbook/assets/Display Name and Email Address.png>)
6. Select the **Allow All Profiles to Use this From Address** option to make it available to all profiles.\
   ![](<../.gitbook/assets/Allow All Profiles.png>)
7. Click **Save**.

{% hint style="warning" %}
When you click **Save**, the system will send a verification email to the email address that you configured in the previous steps. You need to verify this email address is correct before you can use it. (Verification is mandatory once you set the Organization-wide Address.)
{% endhint %}

## Setting the From email address in the Digital River app

To specify the From address system email in the Digital River app:

1. Click **App Launcher** ![](<../.gitbook/assets/App launcher.png>).&#x20;
2. Type `Digital River App` in the **Search apps and items** field and click **Digital River App**. ![](<../.gitbook/assets/Digital River App Search.png>)
3. Type the email address you used to [set the From address for system-generated email](step-16-configure-the-from-email-address.md#setting-the-from-address-for-system-generated-email) (for example, `support@acme.com`) in the **From Address for System Emails** field.![](<../.gitbook/assets/From Address for System Emails.png>)
4. Click **Save**.
