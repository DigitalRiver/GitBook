---
description: Learn how to install the Digital River WooCommerce extension.
---

# Install the extension

Search for Global Seller Services by Digital River on the WordPress marketplace and install the plugin. To install the WooCommerce plugin:

1. Click [here](https://nam11.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwordpress.org%2Fplugins%2Fglobal-seller-services-for-woocommerce%2F\&amp;data=04%7C01%7Cmmills%40digitalriver.com%7Cf0f4044231564f9e2c4308d97cfea00d%7Cc183d0798e92436b9045b793f607fd04%7C0%7C0%7C637678255324853913%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000\&amp;sdata=smskdb5QKnE1OcwYjy8FjeONPncY0LWIC2jKNG6%2B47U%3D\&amp;reserved=0) to download and activate the `WooCommerce` plugin for WordPress.
2. Clone this repository in `plugins` folder of your WordPress installation.
3.  Move to the cloned directory and run this command:&#x20;

    &#x20;`composer install && npm i && npm run prod`
4. Log in to the admin dashboard and go to `WooCommerce->Settings->Payment(tab)`
5. Among the payment methods, find **Digital River** and enable it. Click the **All payment methods** link to view payment methods outside of WooCommerce payments.
6. Click the **Manage** button next to **Global Seller Services for WooCommerce**.  &#x20;
7. Go to the [Digital River dashboard](https://dashboard.digitalriver.com).
8. The `API Keys` can be found under `Developers -> API Keys`.
9. Set the API version to `2020-12-17`. See [how to update the API version](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/api-keys/updating-your-api-version).
10. Go to **Developers** and select **Webhooks**.
11. Click the **Create webhook** button.
12. Enable the endpoint with the slider at the top of the popup.
13. Enter the Endpoint URL with the following format: [https://YOUR\_DOMAIN\_HERE/digitalriver-webhook](https://your\_domain\_here/digitalriver-webhook)
14. Select **101 of 101** events and click the **Create webhook** button.
15. The Webhook secret key can be found by clicking the **Reveal secret** button for this new webhook.
16. Return to the **WooCommerce admin > Settings > Payment** tab.
17. On the **Settings** page, enter the `API Public key`, `API Confidential key` and `Webhook Secret key`.

Your WooCommerce store is now enabled for Digital River Global Seller Services.&#x20;
