---
description: Keep track of changes and updates to the Commerce API.
---

# Release notes

## 2024/11/13

We added [support for recurring payments](../../payments/supported-payment-methods/) to [Apple Pay](../../payments/supported-payment-methods/apple-pay.md).

## 2023/10/5

* We added a `tax_service_invalid_hsCode_warning` to [Warnings](../../common-shopper-and-admin-apis/warnings-object/200-ok.md#warnings) to let you know when your provided HS code is incorrect when creating a product.
* Digital RIver implemented a new feature that enhances tax calculation for certain US states by [adding ZIP Codes and geocodes support](../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md#us-zip-code-and-geocode). This feature addresses the specific tax calculation needs of regions that rely on geocodes and ZIP Codes. This enhancement will significantly improve tax calculation accuracy for users in regions where both ZIP Codes and geocodes are essential. This feature is available automatically; there is no need to enable anything. We also added the [invalid-postal-code](../../common-shopper-and-admin-apis/error-codes/error-codes-for-shopper-apis/409-conflict.md#invalid-postal-code) to the list of [409 Conflict](../../common-shopper-and-admin-apis/error-codes/error-codes-for-shopper-apis/409-conflict.md) codes.

## 2023/10/3

We added support for tax-inclusive [landed costs](../../shopper-apis/cart/pricing/landed-costs/) with a [pretty price](../../shopper-apis/cart/pricing/landed-costs/tax-included-pretty-price.md). The tax-inclusive landed cost enhancement ensures that the prices specified by the client for the product price and shipping cost become the final prices for the order. Tax-inclusive landed cost includes the following enhancements:

* Users can now [set the product price](../../shopper-apis/cart/pricing/landed-costs/tax-included-pretty-price.md#creating-a-price-list-with-a-pretty-price) and [shipping cost as tax-inclusive](../../shopper-apis/cart/pricing/landed-costs/tax-included-pretty-price.md#setting-the-shipping-cost-to-tax-inclusive) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
* Users can see the landed cost for the shipping charge in the payload.

## 2023/9/28

We added examples for [creating a Digital River-hosted and client-hosted shopper](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md#creating-a-shopper) and [initiating an authenticated session for a Digital River-hosted and client-hosted shopper](../../shopper-apis/oauth/tokens.md#initiating-an-authenticated-session-returning-shopper-or-login-shopper).

## 2023/8/31

* Digital River has recently added [CCAvenue ](../../payments/supported-payment-methods/ccavenue.md)to its payment method options. CCAvenue is a payment processing option for Digital River clients with an Indian bank account. This auto-settle payment method offers various local payment options in India, such as Credit Cards, Wallet, Net Banking, and UPI.
* We added [Testing the CCAvenue p](../../resources/testing-scenarios.md#testing-the-ccavenue-payment-method)ayment method to [Testing scenarios](../../resources/testing-scenarios.md).
* We also added the Payment required columns to the [Supported payment methods](../../payments/supported-payment-methods/) table.

## 2023/8/24

In Commerce API, we added.

* [Payment flow descriptions](../../payments/building-your-workflows/flows-by-payment-type.md) to ensure a smooth payment process for each payment type. These payment flows follow Digital River's recommended best practices.
* An Addendum required column to the [Supported payment methods](broken-reference) table.

## 2023/8/23

We updated the shopper token information for the OAuth [Token ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token)in the [Shopper APIs reference](https://www.digitalriver.com/docs/commerce-shopper-api/).

## 2023/8/22

We added the following reasons to the [validation-error](../../common-shopper-and-admin-apis/error-codes/error-codes-for-shopper-apis/400-bad-request.md#validation-error) in [400 Bad Request](../../common-shopper-and-admin-apis/error-codes/error-codes-for-shopper-apis/400-bad-request.md).

* The total product quantity for the current subscription plan and midterm change exceeds the product quantity restriction.

## 2023/5/22

We have included a guide on how to [handle bulk product uploads asynchronously](../../admin-apis/product-management/bulk-operation/asynchronous-bulk-operations/).

## 2023/5/12

We are excited to announce our new feature, Product Combination Supporting Subscriptions for [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). This feature allows you to include subscription products in a product combination and adjust the price to match your pricing or product combination strategies. [Combining multiple SKUs from different product lines into a single product combination](https://help.digitalriver.com/help/gc/Products/Products/Creating-product-combinations-with-components.htm#top) allows you to recognize revenue for each product line based on the component price. This feature also helps you address compliance concerns and minimize revenue loss from customers trying to break bundle offers and purchase products at a reduced price.

## 2023/5/10

With our [mixed cart](broken-reference) feature, a shopper can create a cart that includes physical and digital products. Our feature uses the landed cost solution to calculate the total cost of your purchase, which is only determined once all items in the cart are deemed eligible. If you need help enabling landed cost and pretty price, don't hesitate to contact your Customer Success Manager for assistance.

## 2023/4/5

*   We enabled GitBook AI, a semantic search tool, on the Documentation Portal.&#x20;

    \
    To find GitBook AI, click the **Search** bar in the upper right corner.&#x20;

    <div align="left">

    <figure><img src="../../.gitbook/assets/search-bar.png" alt=""><figcaption></figcaption></figure>

    </div>

    Type your question in the **Ask or search** field and click **Ask "\{{Search content\}} using GitBook AI**. You can ask GitBook AI anything regarding Digital River features. It will give you plain English answers in seconds. For example, you can ask for an overview of a feature, and GitBook AI will return a quick and concise answer.\
    \
    **Note**: While semantic search can provide robust answers, sometimes the answers may be wrong. If you think the answer is incorrect, use the regular search to locate information."

    <div align="left">

    <figure><img src="../../.gitbook/assets/Ask or search CAPI.png" alt=""><figcaption></figcaption></figure>

    </div>

    Additionally, GitBook AI will provide follow-up questions that you might be interested in.&#x20;

    <div align="left">

    <figure><img src="../../.gitbook/assets/Related queries CAPI.png" alt=""><figcaption></figcaption></figure>

    </div>

    You can also see where GitBook AI found the information and click to read more.

    <div align="left">

    <figure><img src="../../.gitbook/assets/Information locations Commerce API.png" alt=""><figcaption></figcaption></figure>

    </div>

    You can ask for a code snippet for an API.

    <div align="left">

    <figure><img src="../../.gitbook/assets/Product payload example CAPI.png" alt=""><figcaption></figcaption></figure>

    </div>

    You can ask for the steps to perform a specific task.

    <div align="left">

    <figure><img src="../../.gitbook/assets/Perrforming test request CAPI.png" alt=""><figcaption></figcaption></figure>

    </div>
* We added Box Shadow as an [available custom style](../reference/elements/#available-custom-styles) when configuring [custom styles](../reference/elements/#custom-styles) for [DigitalRiver.js with Elements](../../payments/payments-solutions/digitalriver.js/).

## 2023/3/29

*   We made the following enhancements to the Admin APIs service:

    * We added [Order Management](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Refund) to the Admin APIs. This API lets you fetch the complete information for anonymous and authenticated orders with an admin token.&#x20;
    * We added the [Retrieve Invoice API](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Invoice) to the Admin APIs. This API allows you to download invoices for both anonymous and authenticated orders with an admin token. Users can subscribe to the `order.invoice.created` event to receive a notification when an invoice is ready for download.

    To start using the new Admin API services, ask your Digital River representatives to add the service to your key. \
    \
    To receive notifications from the webhook service, enable the webhook service on your site. Contact your Digital River representatives for assistance with the service enablement and configure all self-service webhooks through [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
* We replaced the Commerce API reference with a Commerce API suite that includes the following API references:&#x20;
  * [Shopper APIs reference](https://www.digitalriver.com/docs/commerce-shopper-api/): This API reference provides the resources for an end-to-end e-commerce experience used when our Global Commerce platform is the system of record. The Shopper APIs allow clients to build a storefront, create shopper workflows, operate their store, and display products. For more information, see [Shopper APIs](broken-reference), [Shopper APIs reference](../shopper-apis-reference/), [Common Shopper and Admin APIs](broken-reference), and [Common Shopper and Admin APIs reference](../common-shoppers-and-admin-apis-reference/).&#x20;
  * [Admin APIs reference](https://www.digitalriver.com/docs/commerce-admin-api/): This API allows administrators to programmatically create, update, deploy, and retire products on your storefront, create and edit products in bulk, manage product data, and manage sites and subscriptions. Use the Admin APIs to host the Cart and Checkout pages and manage your products via API. For more information, see [Admin APIs](broken-reference), [Admin APIs reference](../admin-apis-reference/), [Common Shopper and Admin APIs](broken-reference), and [Common Shopper and Admin APIs reference](../common-shoppers-and-admin-apis-reference/).
* We updated the following topics:&#x20;
  * [Getting started ](../../master/getting-started/)
  * [Error codes](../../common-shopper-and-admin-apis/error-codes/)&#x20;
* We added the following information:&#x20;
  * [How to resume cart submission](../../shopper-apis/cart/resuming-cart-submission.md)
  * [Considerations](../../shopper-apis/cart/pricing/landed-costs/#considerations) for [landed costs](../../shopper-apis/cart/pricing/landed-costs/)
  * [Best practice flows by payment type](../../payments/sources/using-the-source-identifier.md#best-practice-flows-by-payment-type)
* We added the following subscription notification enhancements:
  * [Sending an expired credit card notification](../../admin-apis/subscription-management/subscription-notifications/sending-an-expired-credit-card-notification.md)
  * [Sending a subscription renewal reminder](../../admin-apis/subscription-management/subscription-notifications/sending-a-subscription-renewal-reminder-notification.md)
  * [Sending a payment failure notification](../../admin-apis/subscription-management/subscription-notifications/sending-a-payment-failure-notification.md)

## 2023/3/16

Digital River adds Clearpay to the payment method roster! By leveraging Afterpay, your shoppers can buy now and pay for their purchases in 3 interest-free payments over 60 days. Learn how you can add Clearpay [here](../../payments/supported-payment-methods/clearpay.md).

## 2023/3/14

[Amazon Pay](../../payments/supported-payment-methods/amazon-pay.md) is a global digital wallet paving the way for your brand to gain visibility and access to millions of existing Amazon customers. This payment method boasts a highly secure and seamless checkout experience, leveraging saved shipping and payment information in the shopper's Amazon account. As a result, the shopper can complete their transactions in 3 simple clicks and almost twice as fast as other payment options. Digital River supports [Amazon Pay Checkout](../../payments/supported-payment-methods/amazon-pay.md#how-it-works).
