---
description: Learn how to retrieve categories.
---

# Categories

A category is a class of products in a store. They are used to organize products in your catalog to help shoppers locate products and navigate your store or site.

## Getting all categories and subcategories

The [`GET /v1/shoppers/me/categories`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories/get) request retrieves all categories and subcategories. See [Categories query parameters](../../general-resources/shopper-apis-reference/categories.md#categories-query-parameters) for a description of the query parameters.&#x20;

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
{% code overflow="wrap" %}
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

## Getting a category by identifier

The [`GET /v1/shoppers/me/categories/{categoryId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories\~1%7BcategoryId%7D/get) request retrieves a specific category and its subcategories by its category identifier (`categoryId`). See [Categories query parameters](../../general-resources/shopper-apis-reference/categories.md#categories-query-parameters) for a description of the query parameters.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/categories/{categoryId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912100",
  "id": 6912100,
  "locale": "en_US",
  "name": "Shop by Category",
  "displayName": "Shop by Category",
  "shortDescription": "string",
  "longDescription": "string",
  "thumbnailImage": "https://drh1.img.digitalriver.com/DRHM/Storefront/Company/demosft1/images/category/thumbnail/shop_by_category.gif",
  "products": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912100/products"
  },
  "categories": {
    "category": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912300",
        "relation": "https://developers.digitalriver.com/v1/shoppers/CategoriesResource",
        "displayName": "Fitness",
        "products": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/categories/6912300/products"
        }
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting all categories for a specific product

The [`GET /v1/shoppers/me/products/{productId}/categories`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1categories/get) request retrieves all categories and subcategories for a specific product. See [Categories query parameters](../../general-resources/shopper-apis-reference/categories.md#categories-query-parameters) for a description of the query parameters.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/categories' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
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
