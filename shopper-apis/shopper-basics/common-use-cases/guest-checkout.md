---
description: Understanding guest checkout.
---

# Guest checkout

Sometimes, when browsing a site or app, a shopper might add an item to their cart but then leave without completing the purchase. Cart abandonment happens to about 34% of shoppers who are asked to create an account before checking out. To reduce the likelihood of this happening, we can offer shoppers the option to check out as a guest and simplify the checkout process. By doing this, shoppers can still access features like viewing their orders and updating their payment information without creating an account.

## Post-order management flow for guest checkout

1. You [send a notification](../../../admin-apis/subscription-management/subscription-notifications/sending-a-subscription-renewal-reminder-notification.md) to a shopper about their subscription.
2. The notification redirects the shopper to the site or app that displays the solution. \
   \
   **Note**: You determine the solutions such as [order management](../../../admin-apis/order-management/), [subscription management](../../../admin-apis/subscription-management/), [email notification](../../../admin-apis/subscription-management/subscription-notifications/), self-service web page, or app notice and app.
3. The shopper goes to the solution page that contains the subscription summary, where you [create an anonymous guest checkout session](../../oauth/tokens.md#creating-an-anonymous-shopper-session-guest-checkout).&#x20;
4. You [can get the subscription details](../../../admin-apis/order-management/downloading-the-invoice.md#step-1-getting-the-order-details) and decide what information to expose to the shopper. For example, if the shopper lands on a page without signing in, you can limit the information displayed to the shopper.
5. The shopper goes to the subscription order details from the subscription summary page. You can [get the subscription details](../../../admin-apis/order-management/downloading-the-invoice.md#step-1-getting-the-download-information-for-the-orders-invoice) and decide what information to expose to the shopper. For example, if the shopper lands on a page without signing in, you can limit the information displayed to the shopper.&#x20;
6. The shopper can download the invoice PDF from the subscription order details page. You can [get the subscription details](../../../admin-apis/order-management/downloading-the-invoice.md#step-1-getting-the-download-information-for-the-orders-invoice) and decide what information to display to the shopper.
7. From the subscription order details page, the shopper can see all details of their order.
8. The shopper can go to the subscription details page from the subscription summary page.&#x20;
9. The shopper can go to the subscription details page from the subscription order details page.
10. From the subscription details page, the shopper can:
    * Display the subscription orders.
    * Update their payment information.
    * Manually renew the subscription.
    * Update the subscription.&#x20;
11. After updating the subscription (by editing the payment, manually renewing, or updating the subscription):
    * You will receive the relevant webhook.
    * You will receive the relevant SSN.
    * The shopper will receive the pertinent email.
12. After the shopper places the order to renew the subscription manually, the shopper returns to the subscription order details page to check the order status.

## Check the order details

If you are an authenticated shopper, you can conveniently access your order details using either the [`GET /v1/shoppers/me/orders/{orderId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D/get) API or the [`POST /v1/shoppers/order-lookup`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Order-Lookup/paths/\~1v1\~1shoppers\~1order-lookup/post) API. However, checking order details can be a bit complicated for anonymous shoppers. It could prevent you from resuming the anonymous shopper token and accessing your order information.

{% hint style="success" %}
An administrator can easily check the order details for an anonymous shopper using the [`GET /v1/orders/{orderId}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Order/paths/\~1v1\~1orders\~1%7BorderId%7D/get) API.
{% endhint %}

## Cancel the order

You can use [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) to cancel an order or line item if it has not been shipped or fulfilled. If you configured notifications, the shopper receives a cancellation notification.

## An authenticated shopper wants to return the goods

An authenticated shopper can use the [`POST /v1/shoppers/me/orders/{orderId}/returns`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Returns/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1returns/get) API when they want to return goods.

## Query the available refund amount for the order

An administrator can use the [`GET /orders/{orderId}/refunds-available`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds-available/get) API for the available refund amount for an order.

## Refund the order

An administrator can use the [`POST /orders/{orderId}/refunds`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds/post) API to refund the order.
