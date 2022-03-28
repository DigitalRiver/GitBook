---
description: >-
  Learn the basics of the Commerce API, how to obtain your credentials, and
  start making requests.
---

# Getting started

## Basic information

The Commerce API is a [RESTful API](https://restfulapi.net). That means we designed the API to allow you to create, read, update, and delete objects with the`POST`, `GET`, `PUT`, and `DELETE` [HTTP methods](https://www.restapitutorial.com/lessons/httpmethods.html).

The Commerce API speaks mainly in JSON. To ensure the API accepts and processes your requests, you'll typically set the content-type header to `application/json` .

All Commerce API requests are sent to `https://api.digitalriver.com`.

For more information on how Digital River ensures high availability and performance, see our [Service Level Agreement](https://help.digitalriver.com/legal/Legal.htm#SLA).

## Quick start guide

This guide shows you how to start making Commerce API requests. By the end, you'll know how to obtain your API keys, import the [Postman](https://learning.postman.com) collection, and run each request. This collection provides the basic requests necessary to submit a simple order through the Commerce API.

### Step 1: Obtain API credentials

Before you can start making Commerce API requests, you'll need to either contact your account manager or use the [Request Demo](https://www.digitalriver.com/request-demo/) form to request your [API keys](https://www.digitalriver.com/docs/commerce-api-reference/#section/API-Keys).&#x20;

Digital River uses these keys to [authenticate](https://www.digitalriver.com/docs/commerce-api-reference/#section/Authentication) your API requests. The API key you use to authenticate the request determines whether the request is in live mode or test mode.  If you forget to provide your key or use one that is incorrect or outdated, the API returns an error.

### Step 2: Perform a test request

After you obtain your API keys, you'll want to perform some test requests. The following steps demonstrate how to do this:

{% hint style="danger" %}
Make sure you [install Postman](https://www.postman.com/downloads/) before proceeding.
{% endhint %}

1. Go to the [Commerce API Postman Collection](https://github.com/DigitalRiver/commerce-api) page on GitHub.
2. To install the Commerce API Postman Collection, click the **Run in Postman** button and select **Postman for Windows**.
3. Click the ![](../.gitbook/assets/three-dots.png) icon on the Commerce API Quick Start collection you just imported and select **Edit**.
4. In the **Edit Collection** window, select **Variables**.
5. Using the **Current Value** fields, enter the appropriate API key for each variable, and click **Update**.
6. Run each request individually or use the [collection runner](https://learning.postman.com/docs/postman/collection-runs/intro-to-collection-runs/) to run each one sequentially.

Now that you've successfully performed a series of simple test requests, you're ready to take a deeper dive into the Commerce API.
