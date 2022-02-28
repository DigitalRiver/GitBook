---
description: Learn how to configure the Salesforce B2B Commerce App.
---

# Step 3: Configure the Salesforce B2B Commerce App

## Step 3a: Update the General Config Settings <a href="#step-2a-update-the-general-config-settings" id="step-2a-update-the-general-config-settings"></a>

The General Config tab provides information that is used by the app to establish secure connections between the Salesforce B2B Commerce platform and Digital River. This tab also includes information about the default **Ship From** address that will be used in the requests that will be sent to Digital River.

To update the General Config settings:

1. Click **App Launcher** ![](<../.gitbook/assets/applauncher (4) (1).png>).
2. Type `Digital River App` in the **Search apps and items** field.\
   &#x20;![](<../.gitbook/assets/Install DR B2B API Connector5.jpg>)
3. Click **Digital River App**.
4. Your Digital River Business Development Manager will provide your **DR Public Key** and **DR Secret Key**. These keys are unique to your site. For security reasons, the Public key and Secret Key fields will always show up as blank values on the UI screen.
5. Update the Storefront Base URL Mapping configuration for all the storefronts configured in your Organization. This takes in a comma-separated list of mapping between the Storefront Name and the Storefront Base URL.
   * If your Community Site URL includes the Storefront Name, then this URL should be a combination of Community URL along with its Storefront name.\
     Example of multiple storefronts:\
     `{"DefaultStore":"https://example1.force.com/DefaultStore1","DefaultStore3":example3.force.com }` Example of a single storefront:\
     `{DefaultStore":"https://example1.force.com/DefaultStore1"}`
   * If your Community Site URL does not include the Storefront Name, then this URL should be only the Community URL. For example:\
     `https://example1.force.com`\
     ![](../.gitbook/assets/Storefront\_Base\_Url\_Mapping.png)&#x20;
6. All the remaining [fields](step-3-configure-the-salesforce-b2b-commerce-app.md#fields) on this tab can remain the same (OOTB values) or can be updated based on the functionality that needs to be enabled for this Digital River Site. Please check with your Digital River Business Development Manager before updating these values. The default warehouse location can be set by populating the Ship From fields shown on this tab.
7. Click **Save**.
8. Click **Test DR Connection** to verify whether you can successfully connect with the configured Digital River Salesforce B2B Commerce App site. If there are errors, check your settings and try again.

{% hint style="info" %}
**Note**: Do not add a Namespace Prefix to the Static resource file name for the Configurations “DR JS Static Resource Name” and “DR CSS Static Resource Name”.
{% endhint %}

![](../.gitbook/assets/StaticResource\_WithoutNamespace.jpg)

## Step 3b: Update Fulfillment Config settings <a href="#step-2b-update-fulfillment-config-settings" id="step-2b-update-fulfillment-config-settings"></a>

The Fulfillment tab provides information that will be used internally by the app during the fulfillment flow and this tab will be removed in future releases. These settings also define when a particular CC Order can be cancelled.

For example, a CC Order can be cancelled only when:

1. The Digital River Order State on CC Order is `accepted` or `pending_payment` or `in_review` or `blocked`.
2. The DR Order Item state on CC Order Items is either `created` or `cancelled`.

![](<../.gitbook/assets/Install DR B2B API Connector7.jpg>)

{% hint style="warning" %}
Do not modify any of these settings as these are used internally by the app.
{% endhint %}

## Fields <a href="#fields" id="fields"></a>

| Field                               | Description                                                                                                                                                                                                                             |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DR Public Key                       | Digital River public key                                                                                                                                                                                                                |
| DR Secret Key                       | Digital River confidential key                                                                                                                                                                                                          |
| DR Callout Time                     | Web Service Call Time Out in milliseconds                                                                                                                                                                                               |
| DR Render Time                      | This field is deprecated and no longer used                                                                                                                                                                                             |
| DR JS Static Resource Name          | Enter the DigitalRiver.js Static resource name                                                                                                                                                                                          |
| DR CSS Static Resource Name         | Enter the Digital River CSS Static resource name                                                                                                                                                                                        |
| Display Proceed to Payment Button   | Toggle to enable or disable the Proceed to Payment Page button on the Order Review page for Non-Subscription $0 Orders. Users are given an option to proceed to the Payment page or directly place an order from the Order Review page. |
| Display Place Order Button          | Toggle to enable or disable the Place Order button on the Order Review page for $0 Orders. Users can place an order directly from the Order Review page without the need to go to the Payment page.                                     |
| Display PO Number                   | Display the Input Field on the Payment page to capture the PO number.                                                                                                                                                                   |
| Display Upload Tax Certificate Link | Toggle to Enable/Disable the Tax Exempt Link on the User Info page and My Tax Certificates on the My Account page.                                                                                                                      |
| Product Sync Job Notification Email | Email address where the Product Sync Job Notifications will be sent.                                                                                                                                                                    |
| Ship From Address Line 1            | The first line of the address.                                                                                                                                                                                                          |
| Ship From Address Line 2            | The second line of the address.                                                                                                                                                                                                         |
| Ship From City                      | The city of the address.                                                                                                                                                                                                                |
| Ship From State                     | The state, province, or address.                                                                                                                                                                                                        |
| Ship From Country                   | A two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.                                                         |
| Ship From PostalCode                | The postal code.                                                                                                                                                                                                                        |
