---
description: Learn how to configure the Digital River app.
---

# Step 2: Configure the Digital River app

The Digital River app uses the following settings:

* General Config&#x20;
* Product Sync&#x20;
* Fulfillment Config

The **General Config** tab provides settings to establish secure connections between the Salesforce Lightning app and Digital River. This tab also includes information (for example, Ship From Address**,** DR Default Entity, and DR API Endpoint) that will be used in the requests that will be sent to Digital River.&#x20;

The **Product** tab provides the batch job settings for syncing or re-syncing products between Salesforce and Digital River. See [Step 8: Configure and synchronize the products](step-8-configure-and-synchronize-the-products.md) for information on how to sync the products.

The **Fulfillment** tab provides configuration settings for batching fulfillments and cancellations.

## Configure the General Config settings

To configure the **General Config** settings:

1. Click **App Launcher** ![](<../.gitbook/assets/App launcher.png>).&#x20;
2. Type `Digital River App` in the **Search apps and items** field and click **Digital River App**. ![](<../.gitbook/assets/Digital River App Search.png>)
3. Click the **General** tab. This tab includes fields for storing information.&#x20;
4. Enter the values in the following fields, such as the **DR Secret Key**, **DR Public Key**, and other fields to configure the Digital River app.&#x20;
5. Click **Test DR Connection** to verify whether you can successfully connect with the configured Digital River site. If there are errors, check your settings and try again.
6. Click **Save**.

![](<../.gitbook/assets/Digital River App Page.png>)

Use the following fields to store configuration information:

| DR Secret Key                                                                                                     | [Provide your Digital River secret key](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/api-keys/getting-your-api-keys).                                                                            |
| ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DR Public Key                                                                                                     | [Provide your Digital River public key](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/api-keys/getting-your-api-keys).                                                                            |
| DR JS Static Resource                                                                                             | <p>The static resource that points to the DigitalRiver.js file. (Namespace should not be added.)</p><p><strong>Example</strong>: DRJS </p>                                                                                              |
| DR CSS Static Resource                                                                                            | <p>The static resource that points to the Digital River CSS file. (Namespace should not be added.)</p><p><strong>Example</strong>: DRCSS</p>                                                                                            |
| Connector Notification Email                                                                                      | The email address for notifications or exceptions.                                                                                                                                                                                      |
| From Address for System Emails                                                                                    | The email address used to send connector notifications and exceptions.                                                                                                                                                                  |
| [Client Custom CSS Static Resource](../extend-the-salesforce-lightning-app/overriding-digital-river-css.md)       | <p>The static resource that points to the client CSS. <br><strong>Example</strong>: DROverideCSS</p>                                                                                                                                    |
| DR Default Entity                                                                                                 | Default Digital River selling entity                                                                                                                                                                                                    |
| DR API Endpoint                                                                                                   | <p>The Digital River API endpoint.<br><strong>Example</strong>: https://apidigitalriver.com</p>                                                                                                                                         |
| DR API Timeout                                                                                                    | The Digital River API timeout value.                                                                                                                                                                                                    |
| DR Environment name                                                                                               | The environment name (for example, Dev, QA, UAT, Production) used in the email subject for system-generated emails.                                                                                                                     |
| DR Webhook Retry Interval                                                                                         | The number of seconds to wait before the Webhook handler reprocesses the event. Do not specify a value that is more than 30 seconds.                                                                                                    |
| Ship From Address – Country ISO Code                                                                              | The country ISO code for the ship from address.                                                                                                                                                                                         |
| Ship From Address - State ISO Code                                                                                | The state ISO code for the ship from address.                                                                                                                                                                                           |
| Ship From Address - Postal Code                                                                                   | The postal code for the ship from address.                                                                                                                                                                                              |
| Ship From Address - City                                                                                          | The city associated with the ship from address.                                                                                                                                                                                         |
| Ship From Address - Line                                                                                          | The ship from address.                                                                                                                                                                                                                  |
| Ship From Address - Provider Name                                                                                 | The Apex class name that is responsible for resolving the Ship From Address information used in the checkout request ([extension point for Ship From Address](../extend-the-salesforce-lightning-app/extend-the-ship-from-address.md)). |
| [Shipping Choice Info - Provider Name](../extend-the-salesforce-lightning-app/shipping-choice-extension-point.md) | The name of the Apex class that is responsible for `serviceLevel` and description information used in the checkout request.                                                                                                             |

## Configure the Product settings

To configure the Product settings:

1. Click the **Product** tab.
2. Enter the value in the **Batch Schedule Time** and **Batch Size** fields.&#x20;
3. Click **Save**.

![](<../.gitbook/assets/Digital River App Product tab.png>)

The Product Sync **** batch job uses the following configuration settings for its schedule and scope size:

| Field               | Description                                                   |
| ------------------- | ------------------------------------------------------------- |
| Batch Schedule Time | Enter the time in minutes for scheduling the batch job.       |
| Batch Size          | Enter the batch scope size. This value should not exceed 100. |

{% hint style="info" %}
Test the app's configuration after you [configure the Product Sync batch job](step-8-configure-and-synchronize-the-products.md#configure-product-synchronization).
{% endhint %}

## Configure the fulfillment/cancellation settings

To configure the fulfillment and cancellation settings:

1. Click the Fulfillment tab.
2. Complete the fields and click **Save**.

![](<../.gitbook/assets/Digital River App Fulfillment tab.png>)

Fulfillment uses the following settings.

| Field                                                                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Batch Fulfillments](../user-guide/fulfillment-cancellation-flow.md#fulfillment-cancellation-batch-flow) | Valid values are `true` or `false`. If true, all Fulfillment/Cancellation Line Item requests will be batched.                                                                                                                                                                                                                                                                                                                                                    |
| Fulfillment/Cancellation Wait Time                                                                       | Enter the time in minutes for batching fulfillments or cancellations. By default, the wait time is 30 minutes. The connector sends a single fulfillment or cancellation request to Digital River the specified number of minutes after it receives the first LineItem Fulfillment/Cancellation request for an order. If there is more than one request during that time, the connector will batch those requests into a single fulfillment/cancellation request. |
