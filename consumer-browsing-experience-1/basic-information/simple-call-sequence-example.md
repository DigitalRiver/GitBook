---
description: Learn how to get a list of categories.
---

# Simple call sequence example

## Step 1: (Optional). Get an OAuth access token

To get the OAuth access token, use the [POST oauth20/token](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) under the OAuth [Token ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token)resource.

{% tabs %}
{% tab title="Request Sample" %}
```
POST /oauth20/token/ 
{

client_id=a78b756bd47e258841d7f007f3f62a&grant_type=password

}
```
{% endtab %}

{% tab title="Response Body" %}
{% code overflow="wrap" %}
```json
{

    "access_token": "your_access_token",

   "token_type": "bearer",

   "expires_in": "3599",

   "refresh_token": "6131be829ea22ccc5ed1199024ba060bd7ed87e8"

}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 2: Get the categories

To get the top-level categories, use the [GET shoppers/me/categories](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories/get) resource.

Use the access token acquired in step 1 as the [bearer token](https://tools.ietf.org/html/rfc6750) in the Authorization header (see Request sample below). This example request overrides the default text format (XML) for the Commerce API. In the `Accept` header, the format is set to JSON as `application/json`.

The response returns the top-level categories available in the [Categories ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories)resource (see Response sample below). The response returns the default resource fields available for a resource and the `displayName`, `thumbnailImage`, and `products` resource fields. You can expand or filter the response using the [fields or expand query parameters](fields-and-expand-query-parameters.md). The links provided in the response indicate the next possible step you could take in a call sequence.

{% tabs %}
{% tab title="Request " %}
```
GET https://api.digitalriver.com/v1/shoppers/me/categories HTTP/1.1

Header:

Accept: application/json 

Authorization: bearer your_access_token
```
{% endtab %}

{% tab title="Response body" %}
A JSON response object is an unordered set of name-value pairs. The {curly brackets} describe objects. The \[square brackets] describe lists. The Response sample below a list starts on line `4` and ends on line `51`. Text strings must be enclosed by double quotation marks. JSON directly supports number values, so numbers are not treated as strings and are not enclosed by double quotation marks. JSON does not support date-time values; therefore, dates and timestamps are typically formatted as strings.

{% code overflow="wrap" lineNumbers="true" %}
```
    {"categories": {
       "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
       "uri": "http://api.digitalriver.com/v1/shoppers/me/categories",
       "category":    [
                {
             "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366200",
             "displayName": "Books",
             "thumbnailImage": null,
            "products":          {
                "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
                "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366200/products"
             }
          },{
             "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366400",
             "displayName": "Accessories",
             "thumbnailImage": null,
             "products":          {
                "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
                "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366400/products"
             }
          }, {
             "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366700",
             "displayName": "Flyleaf Folio",
             "thumbnailImage": null,
             "products":          {
               "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
                "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366700/products"
             }
          },{
             "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436400",
             "displayName": "Newspapers",
             "thumbnailImage": "http://drh1.img.digitalriver.com/DRHM/Storefront/Company/.../thumbnail/blog2_thumb_image.jpg",
             "products":          {
                "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
                "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436400/products"
             }
          },{
             "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436500",
             "displayName": "Blogs",
             "thumbnailImage": null,
             "products":          {
                "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
                "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436500/products"
             }
          }
       ]
    }}
```
{% endcode %}
{% endtab %}
{% endtabs %}
