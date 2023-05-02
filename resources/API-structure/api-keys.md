---
description: Understand how to use your API keys.
---

# API keys

Digital River uses your account's API keys to authenticate your API requests. Contact your Account Manager to obtain your API keys.

Your account provides separate keys for testing and for running live transactions. You can use these keys when sending API requests in either test or live mode. Resources in one mode cannot change resources in another mode. See [Sending API calls](../../master/getting-started/sending-api-calls.md) for additional information on when to use a shopper token and `/auth`.

Digital River returns an error if you do not include your key when you send an API request or use an incorrect or outdated key.

{% hint style="warning" %}
Rotating API keys is a widely accepted best practice recommended by security experts. Rotating API keys makes tracking usage and detecting suspicious activity easier. **By rotating your API keys regularly**, you can ensure the security and protection of your sensitive information and resources. For assistance rotating your API keys, contact your Customer Success Manager.
{% endhint %}

## Public keys

The public API keys identify your account with Digital River and allow you to create sources.&#x20;

## **Confidential keys**

The confidential (secret) API keys allow you to send an API request to Digital River without restriction. Keep these keys confidential and only store them on your servers. Don't use your confidential key for everything.&#x20;

## Service profiles

The service profile determines how you can use your API keys. The Commerce API supports the following service profile levels:

* **Level 1**–You can only use the API keys in an implementation/evaluation phase (test orders only). This profile creates carts as test orders.
* **Level 2**–You can use the API keys in production (for test and live orders).
* **Level 3**–You can use the API keys in production (for test and live orders). These API keys can create payment options and apply payment methods to a cart. A client can provide credit card details in Commerce API requests.
