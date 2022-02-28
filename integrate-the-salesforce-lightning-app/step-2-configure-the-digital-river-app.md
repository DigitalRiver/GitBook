---
description: Learn how to configure the Digital River app.
---

# Step 2: Configure the Digital River app

The Digital River app uses two settings:

* General Config&#x20;
* Product Sync&#x20;

The **General Config** tab provides information from the app to establish secure connections between the Salesforce Lightning app and Digital River. This tab also includes information (for example, Ship From Address**,** DR Default Entity, and DR API End Point) that will be used in the requests that will be sent to Digital River.&#x20;

The **Product** tab provides relevant batch job settings to sync or re-sync products between Salesforce and Digital River. See [Step 8: Configure and synchronize the products](step-8-configure-and-synchronize-the-products.md) for information on how to sync the products.

### Configure the General Config settings

To configure the **General Config** settings:

1. Select the Digital River app.
2. Click the **General** tab. This tab includes fields for storing information.&#x20;
3. Enter the value in the following fields, such as the **DR Secret Key**, **DR Public Key**, and other fields to configure the Digital River app.&#x20;
4. Click **Test DR Connection** to verify whether you can successfully connect with the configured Digital River site. If there are errors, check your settings and try again.

![](<../.gitbook/assets/General config settings.png>)

The following fields are used to store configuration information:

| **Label**                            | Description                                                                                                                                                                                                                             |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Connector Notification Email         | Email address for notifications or exceptions                                                                                                                                                                                           |
| DR CSS Static Resource               | <p>Static resource pointing to the DigitalRiver.js file (Namespace should not be added.)</p><p>Example: DRJS </p>                                                                                                                       |
| DR Default Entity                    | Default Digital River selling entity                                                                                                                                                                                                    |
| DR JS Static Resource                | <p>Static resource pointing to the DigitalRiver.js file (Namespace should not be added.)</p><p>Example: DRCSS</p>                                                                                                                       |
| DR Public Key                        | Digital River public key                                                                                                                                                                                                                |
| DR Secret Key                        | Digital River secret key                                                                                                                                                                                                                |
| Ship From Address - City             | Ship From Address - City                                                                                                                                                                                                                |
| Ship From Address – Country ISO Code | Ship From Address – Country ISO Code                                                                                                                                                                                                    |
| Ship From Address - Line             | Ship From Address - Line                                                                                                                                                                                                                |
| Ship From Address - Postal Code      | Ship From Address - Postal Code                                                                                                                                                                                                         |
| Ship From Address - State ISO Code   | Ship From Address - State ISO Code                                                                                                                                                                                                      |
| Ship From Address Provider Name      | The Apex class name that is responsible for resolving the Ship From Address information used in the checkout request ([extension point for Ship From Address](../extend-the-salesforce-lightning-app/extend-the-ship-from-address.md)). |
| DR API End Point                     | Digital River API End Point                                                                                                                                                                                                             |
| DR API Time Out                      | Digital River API Time Out                                                                                                                                                                                                              |
| DR Webhook Retry Interval            | The number of seconds to wait before the Webhook handler reprocesses the event. Do not specify a value that is more than 30 seconds.                                                                                                    |
| Fulfillment Retry Limit              | The number of times Fulfillment Requests (Order and Line Level) can fail before the status is changed to `Failed`.                                                                                                                      |
| DR Environment name                  | The environment name (for example, Dev, QA, UAT, Production) used in the email subject for system-generated emails.                                                                                                                     |

### Configure the Product settings

To configure the Product settings:

1. Click the **Product** tab.
2. Enter the value in the **Batch Schedule Time** and **Batch Size** fields.&#x20;

![](<../.gitbook/assets/Product tab.png>)

The **Product Sync** batch job uses the following configurations for its schedule and scope size:

| Field               | Description                                               |
| ------------------- | --------------------------------------------------------- |
| Batch Schedule Time | Enter the time (in minutes) for scheduling the batch job. |
| Batch Size          | Batch scope size (maximum value is 100).                  |

{% hint style="info" %}
Test the app's configuration after the [Product Sync](step-8-configure-and-synchronize-the-products.md#product-synchronization) batch job configuration.
{% endhint %}

****



