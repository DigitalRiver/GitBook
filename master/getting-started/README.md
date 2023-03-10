---
description: >-
  Learn the basics of the Commerce API, how to obtain your credentials, and
  start making requests.
---

# Getting started

This guide shows you how to start making API requests from the Commerce API suite. The Commerce API suite consists of two sets of API collections: [Shopper APIs](broken-reference) and [Admin APIs](broken-reference).

The Shopper APIs allow you to build a storefront, create shopper workflows, operate your store, and display products. All shopper requests require an [API key](../../resources/API-structure/api-keys.md) with permission to use the Shopper APIs and an [anonymous ](../../shopper-apis/oauth/tokens.md#getting-an-anonymous-shopper-token)or [authenticated shopper token](../../shopper-apis/oauth/tokens.md#getting-an-authenticated-shopper-token).                                                                                                                                                &#x20;

An administrator or operator can use the Admin APIs to [manage refunds](../../admin-apis/returns-and-refunds-1/), [subscriptions](../../admin-apis/subscription-management/), [sites](../../admin-apis/sites/), and [products](../../shopper-apis/product-discovery/product-variations.md).  All admin requests require an [API key](../../resources/API-structure/api-keys.md) with permission to use the Admin APIs. Note that you can get an API key that [provides permission to use both the Shopper APIs and the Admin APIs](./#step-1-obtain-api-credentials).

By the end, you'll know how to obtain your API keys, import the [Postman](https://learning.postman.com/) collections, and run each request. The collections provide the basic requests necessary to submit a simple order through the Commerce API.

### Step 1: Obtain API credentials

Before you start sending Commerce API requests, use the [Request Demo](https://www.digitalriver.com/request-demo/) form to start the site creation process and request your [API keys](../../resources/API-structure/api-keys.md) or contact your account manager.&#x20;

* To access Commerce API on a trial basis, state that you need a "test API key for the Commerce API suite."&#x20;
* To access the Shopper APIs and the Admin APIs collections, state that your "keys need permission to use both the Shopper APIs and the Admin APIs."

Digital River will reach out to you with more information. If you already have a Commerce API account, you can use your secret key to begin making API calls as well.

Digital River uses these keys to [authenticate ](https://www.digitalriver.com/docs/commerce-shopper-api/#section/Authentication)your API requests. The API key you use to authenticate the request determines whether the request is in live mode or test mode.  If you forget to provide your key or use an incorrect or outdated key, the API returns an error.

### Step 2: Perform a test request

After you obtain your API keys, you'll want to perform some test requests. The following steps demonstrate how to do this:

{% hint style="danger" %}
Make sure you [install Postman](https://www.postman.com/downloads/) before proceeding.
{% endhint %}

1. Go to the [Commerce API Postman collection](https://github.com/DigitalRiver/commerce-api) page on GitHub and follow the instructions to install the API demo collection.&#x20;
2. Complete the following steps:
   1. Click the **View more actions** (<img src="../../.gitbook/assets/three-dots.png" alt="" data-size="line">) icon on the Commerce API Quick Start collection you just imported and select **Edit**.
   2. In the **Edit Collection** window, select **Variables** tab.
   3. Using the **Current Value** fields, enter the appropriate API key for each variable, and click **Update**.
      * **apiDomain**: For the production environment, enter `api.digitalriver.com` in the **Current Value** field. For the client test environment (CTE) enter `api-cte-ext.digitalriver.com` in the **Current Value** field.
      * **publicApiKey**: Provide the public API key provided by Digital River in the **Initial Value** and **Current Value** fields.
      * **drjsApiKey**: Provide the DigitalRiver.js key provided by Digital River in the **Initial Value** and **Current Value** fields.
      * **confidentialApiKey**: Provide the confidential API key provided by Digital River in the **Initial Value** and **Current Value** fields.
      * **confidentialSecret**: Provide the confidential secret provided by Digital River in the **Initial Value** and **Current Value** fields.
   4. Once you set up the variables, run each request individually or use the [collection runner](https://learning.postman.com/docs/postman/collection-runs/intro-to-collection-runs/) to run each request sequentially.

Now that you've successfully performed a series of simple test requests, you're ready to take a deeper dive into the Commerce API.

## Contact us

If you have questions or concerns or if you want to move forward with Digital River, please visit our website at [https://www.digitalriver.com/ ](https://www.digitalriver.com/)and click **Talk To Sales**.
