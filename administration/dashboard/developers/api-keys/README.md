---
description: Learn how to manage your API keys.
---

# API keys

Your account provides separate keys for testing and for running live transactions. You can use these keys when sending API requests in either test or live mode. Resources in one mode cannot change resources in another mode.

You can apply a different API version to each individual key, or you can update the version on all keys simultaneously in the current mode (test or production).

Digital River uses your account's API keys to authenticate your API requests. If you do not include your key when you send an API request or use an incorrect or outdated key, Digital River returns an error.

## Keys and versioning

Use the **Update version on all keys** button on the Keys and versioning pane to [select a version and update all keys to that version](updating-your-api-version.md). You can select to update all API keys to the latest API version or a previous API version. When you update all keys, the API version column for standard keys and restricted keys displays the version you selected.

<figure><img src="../../../../.gitbook/assets/1 Keys and versioning.png" alt=""><figcaption></figcaption></figure>

## Standard keys

Digital River provides each account with four standard keys: a public and confidential (secret) pair for both test mode and live mode. You can use these keys to authenticate Digital River API requests. You cannot create, edit, or delete standard keys, but you can [update ](changing-the-api-version-for-your-standard-key.md)or [rotate them](rotating-keys.md). ‌

The public API keys identify your account with Digital River and allow you to create sources. You can use them with [Drop-in payments](../../../../payments/payment-integrations-1/drop-in/) and [DigitalRiver.js](../../../../payments/payment-integrations-1/digitalriver.js/).

The confidential (secret) API keys allow you to send an API request to Digital River without restriction. Keep these secret keys confidential and only store them on your servers.

<figure><img src="../../../../.gitbook/assets/2 Standard Keys.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**: Limit access to your API keys and secrets to those who need them. Do not store them in a version control system.
{% endhint %}

## Restricted keys

Restrict API keys when you want to limit an application, batch job, or partner to a specific API version. You can also use it to allow your teams to choose when they want to upgrade their API version. You can [create](creating-a-restricted-key.md), [edit](editing-a-restricted-key.md), [delete](deleting-a-restricted-key.md), and [rotate restricted keys](rotating-keys.md).

<figure><img src="../../../../.gitbook/assets/3 Restricted Keys (1).png" alt=""><figcaption></figcaption></figure>
