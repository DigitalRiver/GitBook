---
description: Learn more about the orders resource.
---

# Orders

An _order_ represents a business transaction between two parties. An order typically consists of a collection of line items, billing address, and shipping address.

The [Orders ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders)resource provides access to an authenticated shopper's orders. Use the Orders API to get order details for a shopper.

{% hint style="warning" %}
**Important**: All methods in this API require an authenticated (full access) token.
{% endhint %}

<figure><img src="../../../.gitbook/assets/Digital_River_Demo_Online_Store_Order_Details (1).png" alt=""><figcaption></figcaption></figure>

## Orders query parameters

The following describes the query parameters for [orders](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides other fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Order state

The `orderState` specifies the state of the order. The possible values are as follows: `Open`, `In Process`, `Cancelled`, `Submitted`, `Complete`, `Dispute`, `In Review`, `Source Pending Funds`, `Source Pending Redirect`, and `Charge Pending`.

### Page number

The `pageNumber` specifies the page to display from the results page. The default is `10`. Only available for [`GET /v1/shoppers/me/orders`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders/get).

### Page size

The `pageSize` specifies the maximum number of items to include on each page. Only available for [`GET /v1/shoppers/me/orders`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders/get).

### Token

The `token` is the authorized or anonymous token for the shopper.

## Order lookup query parameters

The following describes the query parameters for [order-lookup](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Order-Lookup).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides other fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Token

The `token` is the authorized or anonymous token for the shopper.

