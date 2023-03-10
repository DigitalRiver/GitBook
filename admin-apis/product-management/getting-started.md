---
description: Learn how to make Product Admin APIs requests.
---

# Getting started

## Asynchronous and synchronous calls

The Commerce API suite uses both asynchronous and synchronous calls. The [product management APIs](./) send asynchronous API requests to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) when:

* [Creating](manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product), [updating](manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product), [deploying](manage-products-asynchronous-api/deploying-a-product.md), [retiring](manage-products-asynchronous-api/retiring-a-product.md), or [deleting a base or individual product](manage-products-asynchronous-api/deleting-a-base-or-individual-products-locale.md)
* [Adding](manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product), [updating](manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#updating-a-specific-product-variation), or [deleting a product variation](manage-products-asynchronous-api/deleting-a-product-variation.md)
* [Deleting a base or individual product's locale](manage-products-asynchronous-api/deleting-a-base-or-individual-products-locale.md)

All other API requests are synchronous and return data immediately.

Asynchronous calls allow you to send multiple requests in a small timeframe without waiting for the completion of a request or worrying about timeouts. These calls are sent to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) to process product requests. Most products will complete successfully within a few seconds. However, it will take longer to create or update a base product with many variations and locales. For example, creating a base product with 10 variations and 55 locales will take 30 seconds to a minute to complete.&#x20;

When Global Commerce receives an asynchronous request, it returns a task identifier (`taskId`) in the response and puts the request in a queue. You can use the `taskId` in synchronous requests to [retrieve product information](retrieve-products-synchronous-api/) and [get the current status of a product](get-the-task-status-for-a-product-synchronous-api/).

## Step 1: Obtain API credentials

When you get your credentials, make sure your API keys have [permission to use the Admin APIs](../../master/getting-started/#step-1-obtain-api-credentials).

## Step 2: Manage your products

{% hint style="info" %}
Steps marked with Async below indicate the request goes to [Global Commerce,](https://gc.digitalriver.com/gc/ent/login.do) where it is [added to a queue](get-the-task-status-for-a-product-synchronous-api/). The remaining steps are synchronous and applied immediately.
{% endhint %}

1. Get your [private key (secret)](../../resources/API-structure/api-keys.md#private-keys). You will need the private key to send calls to the Admin APIs.
2. Async. Create a new product. You can [create an individual product](manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product), a [base product](manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product), or a [product with variations](manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product).
3. [Verify the successful completion of the task](get-the-task-status-for-a-product-synchronous-api/) when creating or updating a product.\
   **Note**: You cannot apply additional changes to the product until the system completes the previous task.
4. Choose one of the following options:
   * Async (deployment needed). [Update a base product or individual product](manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product). You can update any supported attribute for a base or individual product. The change is visible to the shopper on the next deployment.
   * Async (deployment needed). [Add or update a product variation](manage-products-asynchronous-api/adding-or-updating-a-product-variation.md). You can add or update any supported attribute for a product variation. The change is visible to the shopper on the next deployment.
   * Async (live change). [Apply a live change to an individual product, base product, or product variation](manage-products-asynchronous-api/applying-live-changes.md). Update any supported attribute for an individual product, base product, or product variation. The change is visible to the shopper immediately upon the successful completion of the request.
   * Async. [Delete a specific locale](manage-products-asynchronous-api/deleting-a-base-or-individual-products-locale.md) or [delete a product variation](manage-products-asynchronous-api/deleting-a-product-variation.md). Update any supported attribute for an individual product or base product or remove a product variation. The change is visible to the shopper immediately upon the successful completion of the request.
5. Sync. [Query tasks by task identifier, product identifier, or ERID](get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-multiple-products). If you are using ERID, note that the request searches for tasks currently associated with the ERID.\
   **Note**:  Ensure all create and update requests are completed successfully or failed. You cannot deploy or retire a product before the task completes.
6. Async. [Deploy the product](manage-products-asynchronous-api/deploying-a-product.md).
7. Async. [Retire the product](manage-products-asynchronous-api/retiring-a-product.md).

## Step 3: Retrieve product information

{% hint style="info" %}
The following steps are synchronous and applied immediately.
{% endhint %}

Choose one or more of the following options:

* Sync. [Get product information](retrieve-products-synchronous-api/getting-a-base-or-individual-product.md). The response only returns supported attributes. All product variations (if any) for a base product will appear as a URL in the response.
* Sync. [Get product information limited to a single locale](retrieve-products-synchronous-api/getting-a-product-variation.md). The response only returns supported attributes. All product variations (if any) for a base product will appear as a URL in the response.
* Sync. [Get product variation information](retrieve-products-synchronous-api/getting-a-product-variation.md). The response only returns supported attributes.&#x20;
* Sync. [Get product variation information limited to a single locale](retrieve-products-synchronous-api/getting-a-product-variation-by-locale.md). The response only returns supported attributes. The `localizations` object will only display information for the locale specified in the URL path.
