---
description: Learn how to get a list of categories.
---

# Simple call sequence example

### Step 1: (Optional). Get an OAuth access token

To get the OAuth access token, use the [POST oauth20/token](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) under the OAuth [Token ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token)resource.

{% tabs %}
{% tab title="Request Sample" %}
{% code overflow="wrap" %}
```
POST /oauth20/token/ 
{

client_id=a78b756bd47e258841d7f007f3f62a&grant_type=password

}
```
{% endcode %}
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

### Step 2: Get the categories

To get the top-level categories, use the [GET shoppers/me/categories](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories/get) resource.

Use the access token acquired in step 1 as the [bearer token](https://tools.ietf.org/html/rfc6750) in the Authorization header (see Request sample below). This example request overrides the default text format (XML) for the Commerce API. In the `Accept` header, the format is set to JSON as `application/json`.

The response returns the top-level categories available in the [Categories ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories)resource (see Response sample below). The response returns the default resource fields available for a resource and the `displayName`, `thumbnailImage`, and `products` resource fields. You can expand or filter the response using the [fields or expand query parameters](fields-and-expand-query-parameters.md). The links provided in the response indicate the next possible step you could take in a call sequence.

{% tabs %}
{% tab title="Request Sample" %}
{% code overflow="wrap" %}
```
GET https://api.digitalriver.com/v1/shoppers/me/categories HTTP/1.1

Header:

Accept: application/json 

Authorization: bearer your_access_token
```
{% endcode %}
{% endtab %}

{% tab title="Response Sample" %}
{% code overflow="wrap" %}
```json
1.  {"categories": {
2.     "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
3.     "uri": "http://api.digitalriver.com/v1/shoppers/me/categories",
4.     "category":    [
5.              {
6.           "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
7.           "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366200",
8.           "displayName": "Books",
9.           "thumbnailImage": null,
10.          "products":          {
11.             "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
12.             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366200/products"
13.          }
14.       },{
15.          "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
16.          "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366400",
17.          "displayName": "Accessories",
18.          "thumbnailImage": null,
19.          "products":          {
20.             "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
21.             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366400/products"
22.          }
23.       }, {
24.          "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
25.          "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366700",
26.          "displayName": "Flyleaf Folio",
27.          "thumbnailImage": null,
28.          "products":          {
29.            "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
30.             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/38366700/products"
31.          }
32.       },{
33.          "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
34.          "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436400",
35.          "displayName": "Newspapers",
36.          "thumbnailImage": "http://drh1.img.digitalriver.com/DRHM/Storefront/Company/.../thumbnail/blog2_thumb_image.jpg",
37.          "products":          {
38.             "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
39.             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436400/products"
40.          }
41.       },{
42.          "relation": "http://developers.digitalriver.com/v1/shoppers/CategoriesResource",
43.          "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436500",
44.          "displayName": "Blogs",
45.          "thumbnailImage": null,
46.          "products":          {
47.             "relation": "http://developers.digitalriver.com/v1/shoppers/ProductsResource",
48.             "uri": "http://api.digitalriver.com/v1/shoppers/me/categories/40436500/products"
49.          }
50.       }
51.    ]
52. }}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Reading a JSON response

A JSON response object is an unordered set of name-value pairs. the {curly brackets} describe objects. The \[square brackets] describe lists. The Response sample above starts a list on line `4` and ends it on line `51`. Text strings must be enclosed by double-quotes. JSON directly supports number values, so numbers are not treated as strings and are not enclosed by double-quotes. JSON does not support date-time values; therefore, dates and timestamps are typically formatted as strings.
