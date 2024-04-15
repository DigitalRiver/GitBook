---
description: >-
  Learn how to configure a Prebuilt Checkout session and create one-time and
  reusable Prebuilt Checkout links.
---

# Prebuilt Checkout

You can configure Prebuilt Checkout to generate links that connect to an upstream commerce system with Digital River's payment processing, fraud detection, tax exemption, and disclosure services.

The Digital River Dashboard provides the following features to let you use this capability:

* A configuration settings page that lets you create, save, and manage Prebuilt Checkout scoped configurations. This topic focuses on how to use this page. The Prebuilt Checkout page is found under the Settings section.
* A related link generation page that lets [you create a Prebuilt Checkout session and generate checkout links](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md) after you have created a configuration.

{% hint style="info" %}
**Note:** You can access all or part of the Prebuilt Checkout feature based on your assigned role for using the Dashboard.

If you are assigned a Customer Service role, you can do the following:

* [Create a Prebuilt Checkout link session](prebuilt-checkout.md#create-a-prebuilt-checkout)
* [View](prebuilt-checkout.md#work-with-prebuilt-checkout-links) link information and the Prebuilt Checkout link details.
* Create a Prebuilt Checkout link session by [clicking **Add link**](prebuilt-checkout.md#add-a-link).
* [Generate](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md) a one-time Prebuilt Checkout link that expires in 24 hours.&#x20;
* [Generate ](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md)a reusable Prebuilt Checkout link with no expiration.
* [Add a new or existing product](../order-management/prebuilt-checkout-links/add-a-product-during-prebuilt-checkout.md) to a Prebuilt Checkout link.
* [Add a new or existing customer](../order-management/prebuilt-checkout-links/add-a-customer-during-prebuilt-checkout.md) to a Prebuilt Checkout link.

If you are assigned an Administrator role, you can do the following with this feature:

* [Create, save, update, and manage Prebuilt Checkout scoped configurations](prebuilt-checkout.md).
* [Create a Prebuilt Checkout link session](prebuilt-checkout.md#create-a-prebuilt-checkout).
* [View](prebuilt-checkout.md#work-with-prebuilt-checkout-links) link information and the Prebuilt Checkout link details.
* [Generate](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md) a one-time Prebuilt Checkout link that expires in 24 hours.&#x20;
* [Generate ](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md)a reusable Prebuilt Checkout link with no expiration.
* [Delete any one-time _or_ reusable Prebuilt Checkout link they no longer want to be active.](../order-management/prebuilt-checkout-links/generate-prebuilt-checkout-links.md)

For more information on roles, refer to [Users and roles](users-and-roles/).
{% endhint %}

## Understand the uses of Prebuilt Checkout

The configurable Prebuilt Checkout session is helpful if you have limited storefront capabilities but still need to complete order checkouts.&#x20;

Once you build a cart and initiate a checkout, the Prebuilt Checkout feature handles the rest of the transaction and presents you with a link to a checkout modal to let you complete the purchase.&#x20;

You can use this feature to:

* Create a checkout method so you do not depend on a storefront presence.
* Create a checkout method if you do not have a storefront but a product catalog with SKUs to enter to sell those items.
* Generate a one-time use checkout link if you are running a temporary promotion. Both administrators and customer service representatives can generate one-time-use links.
* Generate a _reusable_ checkout link if running an extended or permanent promotion. You must have an Administrator role to create a reusable link.
* Generate a Prebuilt Checkout link, which you can copy and paste anywhere. For example, the link could be copied to an email or a social media post to provide a quick purchase and checkout.
* Provide a checkout method if you want to continue selling products but have a temporarily disabled storefront site or a site under construction.

## Create a Prebuilt Checkout

If assigned an Administrator role, you can create and save a Prebuilt Checkout configuration with editable settings that let you define future Prebuilt Checkout session link requests.&#x20;

An Administrator can create, save, update, or replace a scoped configuration for the Prebuilt Checkout feature. This configuration includes default shipping settings, consents, policies, links, and more that can be configured to appear in the checkout modal UI presented in a subsequent Prebuilt Checkout session. With this saved configuration, you do not need to specifically enter Prebuilt Checkout configuration information every time you want to initiate a new session.&#x20;

Once a Prebuilt Checkout configuration has been created and saved, administrators and customer service representatives can then request one-time use checkout links using that session ID. The Prebuilt Checkout session ID and URL provided in a session response create a one-time checkout modal window. If you have an Administrator role, you can also decide whether the link is either single-use or reusable.

## Select the options and settings for your Prebuilt Checkout configuration

Before creating and saving your Prebuilt Checkout configuration, choose the options and settings you want to save in your configuration. Use the following steps:

1. &#x20;Go to **Settings** in the left navigation of the Dashboard and click **Prebuilt Checkout** to go to the correct page.&#x20;
2.  Choose your options and settings from the following selections:\


    <figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The following sections describe each option and setting.

### Custom options&#x20;

Enable or disable the following custom options by toggling the settings:

* Display a "Purchasing for a Business" checkbox: Enable this option to display a "Purchasing for a Business" checkbox on your configuration page. Selecting this checkbox indicates that the shopper purchases for a business rather than an individual.
* Require shoppers to provide a ship to phone number: Enable this option to require the shopper to give a  ship-to phone number during checkout.
* Require shoppers to provide a bill to phone number during checkout: Enable this option to require the shopper to give a bill-to phone number.

### Logistics&#x20;

Pick your shopper's logistics settings by selecting the appropriate checkbox:

* Set a default shopping country: Sets the shopper's default shopping country.
* Set a default ship from address: Sets the shopper's default ship-from address.
* Default ship from country: Sets the shopper's default ship-from country.
* Set default shipping methods: Lets the shopper specify default shipping methods.

### Shopper consents

Pick your shopper's consent settings by selecting the appropriate checkbox:

* Display additional legal policies: Provides a clickable link to the store's other legal policies at checkout.
* Display marketing opt-in checkbox: Provides you with a selectable checkbox that lets the shopper opt-in to the store's marketing information.

### Store policies&#x20;

Pick your shopper's store policies settings by selecting the appropriate checkbox:

* Display a link to your store's return policy: Provides a clickable link to the store's return policy at checkout.
* Display a link to your store's refund policy: Provides a clickable link to the store's refund policy at checkout.

### Webhooks&#x20;

Pick your shopper's webhook settings by selecting the appropriate checkbox:

* Enable the shipping webhook: Turns on the [shipping webhook feature](prebuilt-checkout.md#configure-a-shipping-callout).
* Enable the store credit webhook: Turns on the [store credit webhook feature](prebuilt-checkout.md#configure-a-store-credit-callout).

## Create the Prebuilt Checkout configuration

The Prebuilt Checkout page is where you create, save, update, or replace a scoped configuration used by the Prebuilt Checkout feature.&#x20;

Once you have chosen the options you want in your configuration, create the configuration by saving the settings and options.

To create a new Prebuilt Checkout configuration or manage an existing configuration, go to **Settings** in the left navigation of the Dashboard and click **Prebuilt Checkout** to go to the correct page. Make sure that you have already chosen your options and settings. The following is an example of a Prebuilt Checkout page with chosen settings:\


<figure><img src="../../../.gitbook/assets/2 pbco settings save.png" alt=""><figcaption></figcaption></figure>

Use the following steps to create a new Prebuilt Checkout configuration on the Prebuilt Checkout page:

1. Under **Logistics**, Add your [**Default ship from address** ](https://docs.digitalriver.com/digital-river-api/integration-options/drop-in-checkout/defining-the-drop-in-checkout-session#ship-from)in the provided fields. This address will be the one to ship physical products from.
2. Add your [**Default shipping methods**](https://docs.digitalriver.com/digital-river-api/integration-options/drop-in-checkout/defining-the-drop-in-checkout-session#ship-from) information**.** In the fields provided, add the **Amount** (for example, 5.00), **Description**, and **Service level** of each **Default shipping method** to be used. Default shipping method information must be entered to cover the physical products being sold. Click **Add row** to add each additional shipping method you want to use.\
   \
   **Note:** Enter **Amount** information as decimal values.
3. [Add optional **Shipping callout**](prebuilt-checkout.md#configure-a-shipping-callout) information. You can configure a shipping callout endpoint for Prebuilt Checkout in this section. Use this feature to configure a shipping method for a Prebuilt Checkout if you do not already have default methods configured. Refer to [Configure a shipping callout](prebuilt-checkout.md#configure-a-shipping-callout) for complete information.\
   \
   **Note:** After customers submit shipping information, we pass their address (along with the checkout session’s product data) in a [`POST/checkout/shipping-quote`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShippingMethodQuotes). The shipping callout endpoint you provide must be able to receive and handle this request and [send a reply that adheres to the response contract](https://app.swaggerhub.com/apis/DigitalRiverX/dropin-checkout/master#/Drop-in%20Shipping%20Quotes/listShippingMethodQuotes).
4. [Add optional **Store credit callout**](prebuilt-checkout.md#configure-a-store-credit-callout) information in this section of the Prebuilt Checkout page. When you do this, each time a shopper requests to use store credit, Digital River checks to see if there is a saved endpoint. With the callout configured, the `POST /drop-in/checkout-sessions` call calls the store credit callout endpoint URL to check if the amount is valid.
5. Under **Consents**, provide the following information:
   1. &#x20;**Company name** that you want to appear on the checkout modal.
   2. **Email promotions URL** to provide links to promotions in the checkout modal.
   3. **EULA URL** to provide the end-user license agreement text in the checkout modal.
   4. **Terms of Service URL** to provide the company Terms of Service text in the checkout modal
6. Under the **Policies** subsection, provide the following information:
   1. **Return Policy URL** to provide a link to the company return policy information in the checkout modal.
   2. **Refund policy URL** to provide a link to the company return policy information in the checkout modal.
7. Click **Save** to save your Prebuilt Checkout configuration settings, or click **Cancel** to discontinue this task.

{% hint style="info" %}
**Note:** Entering incorrect or invalid information in these fields will result in an error message. This could include entering invalid URLs, data of the wrong type, invalid country codes, etc.
{% endhint %}

### Edit and update an existing Prebuilt Checkout configuration

You can change or update the settings if you previously saved Prebuilt Checkout. Use the following steps to edit or update a current Prebuilt Checkout:\


<figure><img src="../../../.gitbook/assets/3 pbco settings edit.png" alt=""><figcaption></figcaption></figure>

1. Go to **Settings** in the Dashboard left navigation and click **Prebuilt Checkout**.
2. In the previously saved configuration, an **Edit** button appears instead of a Save button in the upper right corner of the **Prebuilt Checkout** configuration page.
3. Click **Edit** to begin editing the information.
4. Change the settings in the page form as needed.
5. Click **Save** to re-save the updated Prebuilt Checkout configuration.

{% hint style="info" %}
**Note:** Entering incorrect or invalid information in these fields will result in an error message. This could include entering invalid URLs, data of the wrong type, invalid country codes, etc.
{% endhint %}

## Configure a shipping callout

You can also configure a shipping callout endpoint for Prebuilt Checkout. The Shipping callout subsection is below this page's Default shipping methods subsection.

The shipping callout is an endpoint provided by a client or connector (because every connector has different options). This allows Prebuilt Checkout to query and provide shipping options directly from the client's or connector platform's shipping settings. The endpoint uses the `sessionId` to get the address data from Prebuilt Checkout and query the platform to get the correct shipping option data to Prebuilt Checkout.

You can use this feature to configure a shipping method for a Prebuilt Checkout session if you do not already have a default method configured. Providing the information requested in this subsection of the page allows you to access your endpoint to bring in your shipping methods during the Prebuilt Checkout process.

Provide the following information:

* **URL** for the shipping callout
* **Username** to authenticate with this URL&#x20;
* **Password** to authenticate with this URL

By entering the Shipping callout information, you override other configured shipping methods used during the `POST /drop-in/checkout-sessions` call. The information you provide appears on the front end in the session link modal.

{% hint style="info" %}
**Note:** After customers submit shipping information, we pass their address (along with the checkout session’s product data) in a [`POST/checkout/shipping-quote`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listShippingMethodQuotes). The shipping callout endpoint you provide must be able to receive and handle this request and [send a reply that adheres to the response contract](https://app.swaggerhub.com/apis/DigitalRiverX/dropin-checkout/master#/Drop-in%20Shipping%20Quotes/listShippingMethodQuotes).
{% endhint %}

## Configure a store credit callout

You can configure a store credit callout endpoint on the **Prebuilt Checkout** page. The **Store credit callout** subsection is located directly below the **Shipping callout** subsection on this page.&#x20;

For details on how to use this feature in [Prebuilt Checkout](../../../integration-options/low-code-checkouts/drop-in-checkout.md), refer to [Offering store credit](../../../integration-options/low-code-checkouts/offering-store-credit.md).&#x20;
