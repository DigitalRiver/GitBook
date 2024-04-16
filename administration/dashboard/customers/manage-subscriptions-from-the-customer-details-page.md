---
description: >-
  Learn how to view and manage customer subscriptions from the Customer Details
  page.
---

# Manage subscriptions from the Customer Details page

Along with viewing the information from the **Customer Details** page just described in this section, you can also view or cancel customer subscriptions from this page. By doing this, you complete these actions without having to call the API directly or having to use an API request tool such as Postman.

Use this feature to:

* View information related to the subscription, including the subscription length, state, billing reminder dates, etc.
* Cancel the customer subscription

{% hint style="info" %}
**Note:** Currently, you can only view a subscription's current state or cancel a specific active subscription to change its state from **Active** to **Canceled**.
{% endhint %}

To use this feature, you must have access privileges that let you view and edit customer information.

The following is an example of the subscription information found in the **Subscriptions** subsection of the **Customer Details** page.

<figure><img src="../../../.gitbook/assets/1 manage subcsrip.png" alt=""><figcaption></figcaption></figure>

For more information on subscriptions, refer to [Managing subscriptions](../../../integration-options/checkouts/subscriptions/).

## View customer subscription information

To view the complete collection of customer subscription information, do the following:

1. Click **All customers** in the left navigation. The **Customers** page appears.
2. Use the [Search](searching-for-customers.md) feature or scroll to find the customer whose information details you want to view.
3. Click the **Customer ID.** The **Customer details** page appears. The customer's current subscription information can be viewed in the **Subscriptions** subsection of the page. Each separate subscription has its own subsection.

The customer subscription information displayed in each subsection is the following:

* Subscription ID
* Plan ID
* Plan name
* State (Active or Canceled)
* Locale
* Tax inclusive
* Contract binding until (date)
* Created time
* Updated time
* Current period end date
* Net invoice date
* Next reminder date
* SKU ID
* Product ID (SKU group)
* Name
* Description
* Qty (quantity)
* Price per item
* Cancel subscription link (cancels a current subscription if clicked on)

## Cancel a customer subscription

To cancel an Active customer subscription, do the following:

1. Click **All customers** in the left navigation. The **Customers** page appears.
2. Use the [Search](searching-for-customers.md) feature or scroll to find the customer whose details you want to view or change.
3. Click the **Customer ID.** The **Customer details** page appears. The customer's current subscription information can be viewed in the **Subscriptions** subsection of the page.
4. Click the **Cancel subscription** link in the section for that subscription. Active cancellation links are blue and underlined.
5.  Click **Cancel subscription** on the **Cancel subscription** modal to confirm and complete your cancellation. Once a subscription has been canceled, its **State** field in the **Subscriptions** summary is changed from **Active** to **Cancelled**. The **Cancel subscription** link is also grayed out so that it cannot be used again.

    <figure><img src="../../../.gitbook/assets/2 manage subcsrip active.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../../.gitbook/assets/3 manage subcsrip cancelled.png" alt=""><figcaption></figcaption></figure>
