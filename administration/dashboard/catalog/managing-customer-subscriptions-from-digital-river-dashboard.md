---
description: Learn how to manage customer subscriptions from the Digital River Dashboard.
---

# Managing customer subscriptions from Digital River Dashboard

Digital River offers a [PSD2 and SCA](../../../payments/psd2-and-sca/) compliant [subscription management](../../../integration-options/checkouts/subscriptions/) service that automatically schedules and processes recurring payments.

You can view and manage current customer subscriptions in the Dashboard from the **Customer details** page. You can do the following with the subscription information found on this page:

* View customer subscription data
* Change the state of a customer subscription (currently from active to cancelled)
* Cancel customer subscriptions&#x20;

Previously, the only way to work with subscriptions was by calling the Digital River API directly or through Postman.  You can now view customer subscription information and cancel subscriptions directly through the Dashboard if you have been assigned one of the following roles:

* Administrators
* Finance managers
* Customer service roles&#x20;

Anyone that is assigned one of these roles can view the following pages:

* [Customers page](../customers/) - lists all customers and provides the customer ID with a link to the **Customer details** page. Use this page to select a customer.
* &#x20;[Customer details page](../customers/viewing-customer-details.md) - displays the customer subscription information as well as customer email address, type, enablement status, creation date, and more. Use this page to cancel a subscription.

## View customer subscription data

You can view customer subscription data and more details from the Customer details page.&#x20;

To view customer subscription data:

1. Click **All customers** in the Dashboard left navigation. The **Customers** page appears.
2. Use the [Search](../customers/searching-for-customers.md) feature or scroll to find the customer whose subscription details you want to view.
3. Click the **Customer ID.** The **Customer details** page appears.
4. In the **Subscriptions** section at the bottom of the **Customer details** page you can see the following subscription details:

![](<../../../.gitbook/assets/subscription\_section\_customer\_details\_active (3).png>)

The section displays the complete details for each subscription. For customers with multiple subscriptions, the **Subscriptions** section has a sub-section for each separate subscription's details - whether **Active** or **Cancelled**.

A **Cancel subscription** link is in each upper-right corner of a subscription's details sub-section. Click this to cancel an active subscription.&#x20;

Subscriptions also display a SKU ID (Or SKU Group) as well as a Product ID. This additional information is useful if a Subscription is comprised of multiple SKUs.

## Change the state of a customer subscription

You currently have the ability to change a subscription's **State** from **Active** to **Cancelled**.

A **Cancel subscription** link is found in the upper-right corner of each subscription's details section. Click on this link to cancel a subscription. The **State** field in the subscription's displayed details will change from **Active** to **Cancelled** to reflect this action.

## Cancel customer subscriptions&#x20;

By cancelling a customer subscription, you discontinue the active period of that subscription and that subscription will no longer renew. For more details on subscription states and behaviors, refer to [Digital River's subscription service](../../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md).

To cancel a customer subscription from the Dashboard:

1. Click **All customers** in the Dashboard left navigation. The **Customers** page appears.
2. Use the [Search](../customers/searching-for-customers.md) feature or scroll to find the customer whose subscription details you want to view.
3. Click the **Customer ID.** The **Customer details** page appears.
4. In the **Subscriptions** section at the bottom of the **Customer details** page, you see the complete details for each subscription. For customers with multiple subscriptions, the Subscriptions section has a sub-section for each separate subscription's details - whether **Active** or **Cancelled**.
5. Click the **Cancel subscription** link in the upper-right corner of a subscription's details section to cancel an active subscription. You receive a **Cancel** modal that lets you **Cancel Subscription** or **Cancel** if you change your mind.

After you click **Cancel Subscription**, you receive a system modal that tells you whether your cancellation was successful (green message window) or unsuccessful (red message window).&#x20;

When your cancellation is successful, the **Cancel subscription** link is "grayed out" and can no longer be used. The **State** field in the subscription's displayed details also changes from **Active** to **Cancelled** to verify the success of the cancellation.

![](<../../../.gitbook/assets/subscription\_section\_customer\_details (1).png>)