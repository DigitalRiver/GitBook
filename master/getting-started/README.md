---
description: >-
  Discover the fundamentals of the Commerce API, acquire your credentials, and
  initiate sending requests.
---

# Getting started

This guide will walk you through making API requests using the Commerce API suite, which comprises two API collections: [Shopper ](broken-reference)and [Admin APIs](broken-reference). The Shopper APIs allow you to create a storefront, manage shopper workflows, operate your store, and display products. To make shopper requests, you will need an [API key](../../resources/API-structure/api-keys.md) with permission to use the Shopper APIs and an [anonymous](../../shopper-apis/oauth/tokens.md#creating-an-anonymous-shopper-session-guest-checkout) or [authenticated token](../../shopper-apis/oauth/tokens.md#initiating-an-authenticated-session-returning-shopper-or-login-shopper).

If you are an administrator or operator, the Admin APIs can be used to [manage refunds](../../admin-apis/refunds/), [subscriptions](../../admin-apis/subscription-management/), [sites](../../admin-apis/sites/), and [products](../../admin-apis/product-management/). You will need an [API key](../../resources/API-structure/api-keys.md) with permission to use the Admin APIs to make admin requests. It's important to note that you can obtain an API key that [provides access to both the Shopper and Admin APIs](./#step-1-obtain-api-credentials).

By the end of this guide, you will know how to obtain your API keys, import the [Postman](https://learning.postman.com/) collections, and run each request. The collections provide the basic requests to submit a simple order through the Commerce API.

## Step 1: Obtain API credentials

Before sending Commerce API requests, use the [Request Demo](https://www.digitalriver.com/request-demo/) form to start the site creation process, request [API keys](../../resources/API-structure/api-keys.md), or contact your account manager.&#x20;

* To access Commerce API on a trial basis, state that you need a "test API key for the Commerce API suite."&#x20;
* To access the Shopper APIs and the Admin APIs collections, state that your "keys need permission to use both the Shopper APIs and the Admin APIs."&#x20;

Digital River will reach out to you with more information. You can use your secret key to make API calls if you already have a Commerce API account.&#x20;

Digital River uses these keys to [authenticate](https://www.digitalriver.com/docs/commerce-shopper-api/#section/Authentication) your API requests. The API key you use to authenticate the request determines whether the request is in live mode or test mode. The API returns an error if you forget to provide your key or use an incorrect or outdated key.

## Step 2: Perform a test request

After you obtain your API keys, you'll want to perform some test requests. The following steps demonstrate how to do this:

{% hint style="danger" %}
Make sure you [install Postman](https://www.postman.com/downloads/) before proceeding.
{% endhint %}

1. Go to the [Commerce API Postman Collection](https://github.com/DigitalRiver/commerce-api) page on GitHub and follow the instructions to install the API demo collection.
2. Complete the following steps:
3. Click the View more actions (<img src="../../.gitbook/assets/three-dots.png" alt="" data-size="line">) icon on the Commerce API Quick Start collection you just imported and select **Edit**.
4. In the **Edit Collection** window, select the **Variables** tab.
5. Using the **Current Value** fields, enter the appropriate API key for each variable, and click **Update**.
   * **apiDomain**: For the production environment, enter `api.digitalriver.com` in the **Current Value** field. For the client test environment (CTE), enter `api-cteext.digitalriver.com` in the **Current Value** field.
   * **publicApiKey**: Provide the public API key provided by Digital River in the **Initial Value** and **Current Value** fields.&#x20;
   * **drjsApiKey**: Provide the DigitalRiver.js key supplied by Digital River in the **Initial Value** and **Current Value** fields.&#x20;
   * **confidentialApiKey**: Provide the confidential API key supplied by Digital River in the **Initial Value** and **Current Value** fields.&#x20;
   * **confidentialSecret**: Provide the confidential secret supplied by Digital River in the **Initial Value** and **Current Value** fields.
6. Once you set up the variables, run each request individually or use the [collection runner](https://learning.postman.com/docs/postman/collection-runs/intro-to-collection-runs/) to run each one sequentially.

Now that you've successfully performed a series of simple test requests, you dive deeper into the Commerce API.

## Contact us

If you have questions or concerns or want to move forward with Digital River, please visit our website at [https://www.digitalriver.com/](https://www.digitalriver.com/) and click **Talk To Sales**.