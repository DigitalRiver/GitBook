---
description: Learn how to make Product Admin API requests.
---

# Getting started

## API flow

{% hint style="info" %}
All request steps marked with Async below go to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) where they [are added to a queue](asynchronous-product-api/verifying-the-successful-completion-of-a-request.md). The remaining request steps are synchronous.
{% endhint %}

1. Get the [private key (secret)](../resources/API-structure.md#private-keys) or [Global Commerce access token](administrator-browser-experience/product-basics/global-commerce-access-token.md). <mark style="background-color:orange;">??? Am I correct to assume you need the Global Commerce access token only for Asynchronous Product API requests? You can use the private key for all synchronous requests. ???</mark>
2. Async. Create a new product. You can [create an individual product](asynchronous-product-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product), [base product](asynchronous-product-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product), or [product with variations](asynchronous-product-api/creating-or-updating-a-product.md).
3. [Verify the successful completion of the task](asynchronous-product-api/verifying-the-successful-completion-of-a-request.md) when creating or updating a product.\
   **Note**: You cannot apply additional changes to the product until the system completes the previous task.
4. Choose one of the following options:
   1. Async. [Update a base product or individual product](asynchronous-product-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product). You can update any supported attribute for a base or individual product. The change is visible to the shopper on the next deployment.
   2. Async. [Adding or updating a product variation](asynchronous-product-api/adding-or-updating-a-product-variation.md). You can add or update any supported attribute for a product variation. The change is visible to the shopper on the next deployment.
   3. Async (live). [Apply a live change to an individual product, base product, or product variation](asynchronous-product-api/applying-live-changes.md). Update any supported attribute for an individual product, base product, or product variation. The change is visible to the shopper immediately upon the successful completion of the request.
   4. Async. [Delete a specific locale](asynchronous-product-api/deleting-a-base-or-individual-products-locale.md). Update any supported attribute for an individual product or base product. The change is visible to the shopper immediately upon the successful completion of the request.
   5. Async (live). [Remove a product variation from its base product](asynchronous-product-api/deleting-a-product-variation.md). The change is visible to the shopper immediately upon the successful completion of the request.
5. [Query tasks by task identifier, product identifier, or ERID](asynchronous-product-api/verifying-the-successful-completion-of-a-request.md). If you are using ERID, not that the request searches for tasks currently associated with the ERID.\
   **Note**:  Ensure all create and update requests are completed successfully or failed. You cannot deploy or retire a product before the task completes.
6. [Deploy the product](asynchronous-product-api/deploying-a-product.md).
7. [Retire the product](asynchronous-product-api/retiring-a-product.md).
8. [Get product information](synchronous-product-api/getting-a-base-or-individual-product.md). Only supported attributes will be returned. All product variations (if any) for a base product will appear as a URL in the response.
9. [Get product information limited to a single locale](synchronous-product-api/getting-a-product-by-locale.md). Only supported attributes will be returned. All product variations (if any) for a base product will appear as a URL in the response.
10. [Get product variation information](synchronous-product-api/getting-a-product-variation.md). Only supported attributes will be returned.&#x20;
11. [Get product variation information limited to a single locale](synchronous-product-api/getting-a-product-variation-by-locale.md). Only supported attributes will be returned. The `localizations` object will only display information for the locale specified in the URL path.
