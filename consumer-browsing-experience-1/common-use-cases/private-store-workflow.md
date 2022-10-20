---
description: Understand the Private Store workflow.
---

# Private Store workflow

## Private Store workflow

This topic describes the private store workflow. This scenario assumes:

* The site uses a public API key.
* The site has multiple private stores to choose from, and the private store ID and its corresponding target market ID are unknown. If you know the private store ID and target market ID information, the search step is optional.
* There is only one access rule configured for authorizing customer by email domain.
* Customer authentication is required to browse within a purchase plan. Authentication is a prerequisite if `isAuthenticationRequiredToBrowse` is set to true.

### How to associate a customer with a private store

1. Optional. Search for a private store.
2. Get an access token.
3. Authorize a customer into the private store.
4. Optional. Add a product to a cart.
5. Optional. Redirect a customer to the Checkout page.

#### Step 1. Search for a private store

Send a GET request with the access rules search criteria for the private store to the [Purchase Plan Search](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Purchase-Plan-Search). Search for available private stores that match the email domain. The search matches criteria based on OR logic. If you configure multiple access rules for a private store, the search can locate private stores based on one valid configured access rule. For instance, if a private store restricts access by both email domain and IP address, you can find the private store by searching for the email domain.

{% tabs %}
{% tab title="Request sample" %}
```http
GET https://api.digitalriver.com/v1/shoppers/me/purchase-plan/search?
emailDomain=university.edu&apiKey=apiKey
```
{% endtab %}

{% tab title="Response sample" %}
```javascript
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
{% endtab %}
{% endtabs %}

#### Step 2. Get an access token

Send a GET request to the Shoppers Token resource. The following request sends a public API key and specifies the JSON format.

{% tabs %}
{% tab title="Request sample" %}
```http
GET https://api.digitalriver.com/v1/shoppers/token?apiKey=yourAPIkey&format=json
```
{% endtab %}

{% tab title="Response sample" %}
```javascript
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
{% endtab %}
{% endtabs %}

#### Step 3. Authorize a customer into the private store

Send a POST request with the access rule criteria in the payload to the [Purchase Plan Authorize](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Purchase-Plan-Authorize) resource. The response returns an empty document with an HTTP Status 204. When the request is successful, the customer can browse and purchase products from the private store. If the private store provides an overall discount for products, the [Products ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products)resource reflects discounted prices, as well as any associated offers. The [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource also reflects discount prices. When the request is unsuccessful, an error message indicates the issue.

{% tabs %}
{% tab title="Request sample" %}
```javascript
POST https://api.digitalriver.com/v1/shoppers/me/purchase-plan/authorize 
```
{% endtab %}

{% tab title="Request body sample" %}
```javascript
{
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
}
```
{% endtab %}

{% tab title="Response sample" %}
```
HTTP/1.1 204 No Content
```
{% endtab %}
{% endtabs %}

Subsequent calls in the workflow could include:

1. Add a product to a cart.
2. Redirect a customer to the Checkout page.
