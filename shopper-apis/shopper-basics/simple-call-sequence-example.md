---
description: Learn how to get a list of categories.
---

# Simple call sequence

## Step 1: (Optional). Creating full-access token

To create a full-access token, use the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post) request and provide the `client_id` and `grant_type` query parameters.

{% hint style="danger" %}
Never expose or visibly display the limited or full access tokens created by the APIs to the shopper (such as plain text in a cookie). If a shopper has access to these tokens, there is the potential they could bypass any restrictions built into the store's frontend and place orders directly on our systems via our publicly documented APIs.
{% endhint %}

You can only use [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post) when Digital River maintains the shopper's login and password credentials. If the Digital River partner maintains the shopper's login and password credentials, see [Creating a grant OAuth for client credentials](../oauth/tokens.md#creating-a-grant-oauth-flow-for-client-credentials).

{% tabs %}
{% tab title="cURL " %}
{% code overflow="wrap" %}
```json
curl --location --request POST 
'https://api.digitalriver.com/oauth20/token?client_id={clientId}&grant_type={password}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="Response body" %}
{% code overflow="wrap" %}
```json
{
  "access_token": "your_access_token",
  "token_type": "bearer",
  "expires_in": "3599"
  "refresh_token": "your_refresh_token"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 2: Get the categories

To get the top-level categories, use the [GET shoppers/me/categories](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories/get) resource.

Use the access token acquired in step 1 as the [bearer token](https://tools.ietf.org/html/rfc6750) in the Authorization header (see Request sample below). This example request overrides the default text format (XML) for the Commerce API. In the `Accept` header, the format is set to JSON as `application/json`.

The response returns the top-level categories available in the [Categories ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories)resource (see Response sample below). The response returns the default resource fields available for a resource and the `displayName`, `thumbnailImage`, and `products` resource fields. You can expand or filter the response using the [fields or expand query parameters](../../general-resources/common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md). The links provided in the response indicate the next possible step you could take in a call sequence.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/categories' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
A JSON response object is an unordered set of name-value pairs. The {curly brackets} describe objects. The \[square brackets] describe lists. The Response sample below a list starts on line `3` and ends on line `11`. Text strings must be enclosed by double quotation marks. JSON directly supports number values, so numbers are not treated as strings and are not enclosed by double quotation marks. JSON does not support date-time values; therefore, dates and timestamps are typically formatted as strings.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/categories",
  "category": [
    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912100",
      "displayName": "Shop by Category",
      "products": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912100/products"
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
