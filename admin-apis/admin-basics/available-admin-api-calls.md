---
description: Learn about the available Admin API calls.
---

# Available Admin API calls

The following tables list the available Admin API calls.&#x20;

## Refund management

| Path                                  | Details                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/orders/{orderId}/refunds`           | <p><strong>Action</strong>: <a href="../refunds/getting-refunds-for-a-specific-order.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul><p><strong>Action</strong>: <a href="../refunds/creating-a-satisfaction-refund.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                |
| `/orders/{orderid}/refunds/schema`    | <p><strong>Action</strong>: <a href="../refunds/retrieving-the-json-schema-for-an-order-refund.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                                                                                                                                                     |
| `/orders/{orderId}/refunds-available` | <p><strong>Action</strong>: <a href="../refunds/retrieving-refunds-available-for-an-order.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul><p><strong>Action</strong>: <a href="../refunds/retrieving-refunds-available-for-an-order.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul> |

## Subscription management

| Path                                                 | Details                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/v1/subscriptions/{subscriptionId}/activate`        | <p><strong>Action</strong>: <a href="../subscription-management/activating-a-subscription.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                                 |
| `/v1/subscriptions/{subscriptionId}/expiration-date` | <p><strong>Action</strong>: <a href="../subscription-management/updating-the-subscription-renewal-date.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                    |
| `/v1/subscriptions/{subscriptionId}/perpetual-price` | <p><strong>Action</strong>: <a href="../subscription-management/assigning-a-perpetual-unit-price.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                          |
| `/v1/subscriptions/{subscriptionId}/preview`         | <p><strong>Action</strong>: <a href="../subscription-management/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-resource">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>      |
| `/v1/subscriptions/{subscriptionId}/preview-cart`    | <p><strong>Action</strong>: <a href="../subscription-management/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul> |
| `/v1/subscriptions/{subscriptionId}/reference-id`    | <p><strong>Action</strong>: <a href="../subscription-management/changing-the-subscriptions-external-reference-identifier.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                  |
| `/v1/subscriptions/{subscriptionId}/renewal-price`   | <p><strong>Action</strong>: <a href="../subscription-management/changing-the-subscription-renewal-price.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                   |
| `/v1/subscriptions/{subscriptionId}/renewal-product` | <p><strong>Action</strong>: <a href="../subscription-management/changing-the-subscription-renewal-product.md">POST</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul>                                                                 |

## Site management

| Path                                               | Details                                                                                                                                                                                                     |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/v1/sites/{siteId}/authorized-billing-countries`  | <p><strong>Action</strong>: <a href="../sites/getting-a-sites-authorized-shipping-countries.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul> |
| `/v1/sites/{siteId}/authorized-shipping-countries` | <p><strong>Action</strong>: <a href="../sites/getting-a-sites-authorized-shipping-countries.md">GET</a></p><ul><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: No</li></ul> |

## Product management

Note that the `products` in the URL path represent the current product administrator session and the calls that you make to manage products on your online store.

| Path                                                                                                                                                                                                                                                                                              | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/v1/products`                                                                                                                                                                                                                                                                                    | <p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product">POST</a><strong></strong></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: Yes</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `/v1/products/{baseProductId or baseERID}`                                                                                                                                                                                                                                                        | <p><strong>Action</strong>: <a href="../product-management/retrieve-products-synchronous-api/getting-a-base-or-individual-product.md">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul><p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: Yes</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `/v1/products/{baseProductId or baseERID}/locales/{locale}`                                                                                                                                                                                                                                       | <p><strong>Action</strong>: <a href="../product-management/retrieve-products-synchronous-api/getting-a-base-or-individual-product.md">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul><p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: Yes</li></ul><p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/deleting-a-base-or-individual-products-locale.md">DEL</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul>                                                                                                      |
| <p><code>/v1/products/{baseProductId or ERID}/variation/{variationProductId</code> or <code>variationERID}/locales/{locale}</code><br><code></code><br><code></code>OR<br><code></code><br><code>/v1/products/product/variation/{variationProductId or variationERID}/locales/{locale}</code></p> | <p><strong>Action</strong>: <a href="../product-management/retrieve-products-synchronous-api/getting-a-product-variation-by-locale.md#getting-a-product-variation-for-a-specific-base-product-and-locale">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `/v1/products/{baseProductId or baseERID}/deploy`                                                                                                                                                                                                                                                 | <p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/deploying-a-product.md">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> Yes</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `/v1/products/{baseProductId or baseERID}/live-changes`                                                                                                                                                                                                                                           | <p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/applying-live-changes.md#applying-a-live-change-to-a-base-or-individual-product">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> Yes</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| <p><code>/v1/products/{baseProductId or baseERID}/variations/{variationProductId or variationERID}/live-changes</code><br><code></code><br><code>OR</code><br><code></code><br><code>/v1/products/product/variations/{variationProductId or variationERID}/live-changes</code></p>                | <p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/applying-live-changes.md#applying-a-live-change-to-a-product-variation">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> Yes</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| <p><code>/v1/products/{baseProductId or baseERID/variations/{variationProductId or variationERID}</code><br><code></code><br><code></code>OR<br><code></code><br><code>/v1/products/product/variations/{variationProductId or variationERID}</code></p>                                           | <p><strong>Action</strong>: <a href="../product-management/retrieve-products-synchronous-api/getting-a-product-variation.md#getting-a-product-variation-for-a-specific-base-product">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul><p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#updating-a-specific-product-variation">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: YES</li></ul><p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/deleting-a-product-variation.md#deleting-a-product-variation-for-a-specific-base-product">DEL</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul><p></p> |
| `/v1/products/{baseProductId or bbasePaseERID}/retire`                                                                                                                                                                                                                                            | <p><strong>Action</strong>: <a href="../product-management/manage-products-asynchronous-api/retiring-a-product.md">POST</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Async</li><li><strong>Deployment validation</strong>: <strong></strong> No</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `/v1/products/tasks`                                                                                                                                                                                                                                                                              | <p><strong>Action</strong>: <a href="../product-management/get-the-task-status-for-a-product-synchronous-api/#getting-a-list-of-all-tasks">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> Not applicable</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `/v1/products/tasks/{taskId}`                                                                                                                                                                                                                                                                     | <p><strong>Action</strong>: <a href="../product-management/get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-a-specific-task">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> Not applicable</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `/v1/product/tasks?productId={productId)`                                                                                                                                                                                                                                                         | <p><strong>Action</strong>: <a href="../product-management/get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-a-specific-product">GET</a></p><ul><li><strong>ERID support</strong>: Yes</li><li><strong>Mode</strong>: Sync</li><li><strong>Deployment validation</strong>: <strong></strong> Not applicable</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

{% hint style="info" %}
Each paired request below performs the same task:

* `GET /v1/products/product/variations/{productId or ERID}` and  \
  `GET /v1/products/{productId or ERID}/variations/{productVariationId or variationERID}`
* `POST /v1/products/product/variations/{productVariationId or variationERID}` and  \
  `POST /v1/products/{productId or ERID}/variations/{productVariationId or variationERID}`
* `DEL /v1/products/product/variations/{productVariatinId or variatinERID}` and  \
  `DEL /v1/products/{productId or ERID}/variations/{productVariationId or variationERID}`
* `GET /v1/products/{productId or ERID}/locales/{locale}`\
  `GET /v1/products/{productId or ERID}/variation/{productVariationId or variationERID}/locales/{locale}`
{% endhint %}