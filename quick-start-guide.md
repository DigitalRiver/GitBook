---
description: Learn how to how to make Digital River API requests.
---

# Getting started

This guide shows you how to start making Digital River API requests. By the end, you'll know how to set up a Digital River Dashboard account, obtain your API keys, and perform a test request.

## Step 1: Create a test account

Before making Digital River API requests, you must [create a test account](administration/dashboard/quick-start-guide.md#step-1-creating-a-free-test-account) in the [Dashboard](https://dashboard.digitalriver.com/login).

Once you successfully sign in to Dashboard, you can access your account's [API keys](administration/dashboard/developers/api-keys/). Your account is provided with four keys in total: a public and confidential API Key for sending requests in both [test and production modes](administration/dashboard/test-and-production-environments.md). In Dashboard, toggle between **Test** and **Production** to view your public keys and click **Reveal test token** or **Reveal token** to unmask your confidential key.

Digital River uses these keys to authenticate your API requests. The API key you use to authenticate the request determines whether the request is in production mode or test mode. If you forget to provide your key or use one that is incorrect or outdated, the API returns an error.

## Step 2: Perform a test request

You'll want to perform a test request when you have your API keys. The following steps demonstrate how to do this:

{% hint style="danger" %}
Make sure you [install Postman](https://www.postman.com/downloads/) before proceeding.
{% endhint %}

1. Go to the [Digital River API Postman Collection](https://github.com/DigitalRiver/api-sandbox) page on GitHub.
2. To install the Digital River API Postman Collection, click the **Run in Postman** button and select **Postman for Windows**.
3. Click the <img src=".gitbook/assets/three dots.png" alt="" data-size="line">icon on the Digital River Collection you just imported and select **Edit**.
4. In the **Edit Collection** window, select the **Variables** tab.
5. For the **secretKey** variable, paste your confidential test key into the **Initial Value** and **Current Value** fields.
6. Click **Save**.
7. Back in the collection, expand the **Create a Client-fulfilled SKU** folder and open the **Create a physical sku** request.
8. Click **Send**. A successful request creates a [SKU](product-management/skus.md#skus) and the response contains a `201 Created` status code.

![](<.gitbook/assets/SKU request.png>)

## Step 3: Explore integration options

You can dive deeper now that you've successfully performed a simple test request.

To better understand some of Digital River's core services and how to use them, we recommend you look over the [Using our services](using-our-services/) page.

We also offer several integration paths to match your business needs:

* [Low-code checkouts](integration-options/low-code-checkouts/): The quickest, easiest way to integrate. Add a turnkey Digital River-hosted checkout experience with minimal code or construct unique checkout flows with our components.
* [Direct Integrations](integration-options/checkouts/): A more customizable way to build your user experience. Use our ready-to-display features and flexible API suite.
* [Connectors](https://docs.digitalriver.com/partner-integrations/): Pre-built partner integrations allow you to connect with Digital River's payment processing, fraud detection, tax exemption, and disclosure services.
