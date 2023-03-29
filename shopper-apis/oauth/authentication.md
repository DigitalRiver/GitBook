---
description: Learn how Commerce API authenticates requests.
---

# Authentication

The [Shopper APIs](broken-reference) authenticates requests using [API keys](../../resources/API-structure/api-keys.md) and an OAuth token for authentication. The [Admin APIs](broken-reference) only require API keys.

OAuth is an open protocol that provides secure authorization for web, mobile, and desktop applications. A third-party application can use the OAuth 2.0 authorization framework to obtain limited access to an HTTP service.

{% hint style="info" %}
**Note**: Use the OAuth 2.0 authentication exclusively with the Commerce APIs.
{% endhint %}

The Commerce API uses the OAuth 2.0 W3C (World Wide Web Consortium) standard to authenticate and authorize shoppers and their data. OAuth 2.0 allows you, the developer, to access a shopper's account without requiring shoppers to share their account credentials (username and password).

## Consumer-facing applications

Use OAuth to publish and interact with protected data when you are building any of the following consumer-facing applications:

* Website
* Desktop
* Mobile
* Web page widgets
* JavaScript
* Browser-based applications

## Service providers

Use OAuth to give users access to their data while protecting their account credentials when:

* Supporting the web and mobile applications
* Supporting server-side API mashups
* Storing protected data on behalf of your users
