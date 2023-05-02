---
description: Understand the Private Store workflow.
---

# Private Store workflow

This topic describes the private store workflow. This scenario assumes:

* The site uses a public API key.
* The site has multiple private stores to choose from, and the private store ID and its corresponding target market ID are unknown. The search step is optional if you know the private store ID and target market ID information.
* Only one access rule is configured for authorizing the customer by email domain.
* Customer authentication is required to browse within a purchase plan. Authentication is a prerequisite if `isAuthenticationRequiredToBrowse` is set to true.

## How to associate a customer with a private store

1. Optional. [Search for a private store](private-store-workflow.md#step-1.-search-for-a-private-store).
2. [Get an access token](private-store-workflow.md#step-2.-get-an-access-token).
3. [Authorize a customer into the private store](private-store-workflow.md#step-3.-authorize-a-customer-into-the-private-store).
4. Optional. [Add a product to a cart](../../cart/creating-or-updating-a-cart/adding-a-product-to-a-cart.md).
5. Optional. [Redirect a customer to the Checkout page](../../cart/redirecting-to-a-digital-river-hosted-cart.md).

### Step 1. Search for a private store

Send a [`GET /v1/purchase-plan/search`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Search/paths/\~1v1\~1shoppers\~1me\~1purchase-plan\~1search/get) request with the [`emailDomain` query parameter](../../../general-resources/shopper-apis-reference/private-store.md#email-domain) to find the available private stores that match the email domain. The search matches criteria based on OR logic. If you configure multiple access rules for a private store, the search can locate private stores based on one valid configured access rule. For instance, if a private store restricts access by email domain and IP address, you can find the private store by searching for the email domain. See [Private store query parameters](../../../general-resources/shopper-apis-reference/private-store.md#private-store-query-parameters) for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```html
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me/purchase-plan/search? emailDomain=university.edu&apiKey=apiKey' \--header 'Authorization: bearer {{access_token}}' \ 
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
   "purchaseplans": {
      "purchaseplan": {
         "id": "11858700",
         "isauthenticationrequiredtobrowse": "true",
         "purchaseplanname": "Student Discounts",
         "branddisplayname": "",
         "brandlogoimage": "",
         "targetmarketid": "35100",
         "targetmarketname": "Students"
      },
      "totalresults": "1"
   }
}
{
   "purchaseplans": {
      "purchaseplan": {
         "id": "11858700",
         "isauthenticationrequiredtobrowse": "true",
         "purchaseplanname": "Student Discounts",
         "branddisplayname": "",
         "brandlogoimage": "",
         "targetmarketid": "35100",
         "targetmarketname": "Students"
      },
      "totalresults": "1"
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 2. Get an access token

Send a `GET /v1/token` request to the Shoppers Token resource with your public API key and specify the JSON format.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```html
curl --location -g --request GET ' https://api.digitalriver.com/v1/oauth20/token? apiKey=yourAPIkey&format=json' \--header 'Authorization: bearer {{access_token}}' \ 
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
   "token": {
      "access_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b52b...",
      "token_type": "bearer",
      "expires_in": "86397",
      "refresh_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b8f5..."
   }
}
{
   "token": {
      "access_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b52b...",
      "token_type": "bearer",
      "expires_in": "86397",
      "refresh_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b8f5..."
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 3. Authorize a customer into the private store

Send a [`POST /v1/shoppers/me/purchase-plan/authorize`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Authorize/paths/\~1v1\~1shoppers\~1me\~1purchase-plan\~1authorize/post) request with the access rule criteria in the payload. The response returns an empty document with a 204 No content response. When the request is successful, the customer can browse and purchase products from the private store. If the private store provides an overall discount for products, the [Products](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Products) resource reflects discounted prices and any associated offers. The [Cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper) resource also reflects discount prices. When the request is unsuccessful, an error message indicates the issue.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```html
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/purchase-plan/authorize' \
--header 'Authorization: bearer {{access_token}}' \ 
...
--data-raw '{
   "purchasePlanAuthorize": {
      "id": "11858700",
      "targetMarketId": "35100",
      "emailDomain": "university.edu"
   }
 }
 {
    "purchasePlanAuthorize": {
      "id": "11858700",
      "targetMarketId": "35100",
      "emailDomain": "university.edu"
    }
 }'
```
{% endcode %}
{% endtab %}

{% tab title="204 No Content response" %}
{% code overflow="wrap" %}
```
HTTP/1.1 204 No Content
```
{% endcode %}
{% endtab %}
{% endtabs %}

Subsequent calls in the workflow could include:

1. Optional. [Redirect a customer to the Digital River-hosted Checkout page](../../cart/redirecting-to-a-digital-river-hosted-cart.md).
2. Optional. [Add a product to a cart](../../cart/creating-or-updating-a-cart/adding-a-product-to-a-cart.md).
