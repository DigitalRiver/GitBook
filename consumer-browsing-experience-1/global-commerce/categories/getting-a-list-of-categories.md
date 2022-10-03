---
description: Learn how to get a list of categories.
---

# Getting a list of categories

To get a list of categories:

* [Step 1: Get an OAuth action token (optional).](getting-a-list-of-categories.md#step-1-get-an-oauth-access-token-optional)
* [Step 2: Get the categories.](getting-a-list-of-categories.md#step-2-get-the-categories)

## Step 1: Get an OAuth access token (optional)

To get the [OAuth access token](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token), use the `POST /oauth/token` resource. The following example sets the API key to the `client_id` in the POST entity, also called the request body or payload.

{% tabs %}
{% tab title="Request body sample" %}
```http
POST /oauth20/token/ 

{

client_id=a78b756bd47e258841d7f007f3f62a&grant_type=password

}
```
{% endtab %}

{% tab title="Response body sample" %}
```
{

    "access_token": "your_access_token",

   "token_type": "bearer",

   "expires_in": "3599",

   "refresh_token": "6131be829ea22ccc5ed1199024ba060bd7ed87e8"

}
```
{% endtab %}
{% endtabs %}

## Step 2: Get the categories

To get the top-level categories, use the [Categories ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories)resource. Use the access token acquired in [Step 1](getting-a-list-of-categories.md#step-1-get-an-oauth-access-token-optional) as the bearer token in the Authorization header. This example request overrides the default text format (XML) for the Commerce API. In the `Accept` header set the format to `application/json`.

{% tabs %}
{% tab title="Request body example" %}
```http
GET https://api.digitalriver.com/v1/shoppers/me/categories HTTP/1.1

Header:

Accept: application/json 

Authorization: bearer your_access_token
```
{% endtab %}

{% tab title="Response body example" %}
```javascript
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
{% endtab %}
{% endtabs %}
