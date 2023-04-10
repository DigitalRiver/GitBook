---
description: Learn how to provide offers.
---

# Managing offers

## Getting an offer by identifier

You can get a specific offer identifier by submitting a [`GET /shoppers/me/offers/{offerId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1offers\~1%7BofferId%7D/get) request. A successful request returns a `200 OK response`. &#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/offers/{offerId}' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "offer": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709",
    "id": 154344709,
    "name": "Home Page Security & Backup Recovery Features",
    "policyName": "string",
    "type": "FeatureProducts",
    "image": "https://drh1.img.digitalriver.com/DRHM/Storefront/Site/demosft1/images/promo/security_header.gif",
    "trigger": "Always Triggered",
    "salesPitch": [
      "[\"Header Message\",\"Footer Message\",\"Sales Pitch Extra Info\",\"Sales Pitch Extra Info 2\"]"
    ],
    "productOffers": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers",
      "productOffer": [
        {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers/64358400",
          "id": 64358400,
          "product": {
            "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358400",
            "displayName": "Class III",
            "thumbnailImage": "https://drh1.img.digitalriver.com/DRHM/Storefront/Company/demosft1/images/product/thumbnail/classIIIThumb_v2.jpg"
          },
          "pricing": {
            "listPrice": {
              "currency": "USD",
              "value": "19.99"
            },
            "salePriceWithQuantity": {
              "currency": "USD",
              "value": "19.99"
            },
            "formattedListPrice": "$39.99",
            "formattedSalePriceWithQuantity": "$38.99",
            "listPriceIncludesTax": "false"
          }
        }
      ]
    },
    "categoryOffers": {},
    "offerBundleGroups": {}
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting the product for the offer

You can get a specific product for an offer by submitting a [`GET /shoppers/me/offers/{offerId}/product-offers/{productOfferId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1offers\~1%7BofferId%7D\~1product-offers\~1%7BproductOfferId%7D/get) request. A successful request returns a `200 OK response`.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/offers/{offerId}/product-offers/{productOfferId}' \
<strong>--header 'Authorization: Bearer &#x3C;API_key>' \
</strong><strong>...
</strong></code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "productOffer": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers/64358400",
    "id": 64358400,
    "product": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358400",
      "displayName": "Class III",
      "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIIIThumb_v2.jpg"
    },
    "addProductToCart": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=64578500&offerId=154344709",
      "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=64578500&offerId=154344709"
    },
    "salesPitch": "For testing purposes",
    "image": "https://drh-sys-ora.img.digitalriver.com/Storefront/Site/demosft1/images/promo/business_header.gif",
    "pricing": {
      "listPrice": {
        "currency": "USD",
        "value": "19.99"
      },
      "salePriceWithQuantity": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedListPrice": "$39.99",
      "formattedSalePriceWithQuantity": "$38.99",
      "listPriceIncludesTax": "false"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Retrieving all offers for a product

You can get all offers for a specific product by submitting a [`GET /shoppers/me/products/{productId}/offers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1offers/get) request. A successful request returns a `200 OK response`.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/products/{productId}/offers' \
<strong>--header 'Authorization: Bearer &#x3C;API_key>' \
</strong><strong>...
</strong></code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "offers": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/offers",
    "offer": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709",
        "name": "Home Page Security & Backup Recovery Features",
        "trigger": "Always Triggered",
        "productOffers": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers"
        },
        "categoryOffers": {},
        "offerBundleGroups": {}
      }
    ],
    "totalResults": 1,
    "totalResultPages": 1
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Retrieving all offers

You can retrieve all offers for a specific product by submitting a [`GET /shoppers/me/offers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1offers/get) request.&#x20;

The retrieved offers include:

* All always-triggered offers
* All user-triggered promotional URLs and externally triggered offers
* All user-triggered coupon code offers

A successful request returns a `200 OK response`.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/offers' \
<strong>--header 'Authorization: Bearer &#x3C;API_key>' \
</strong><strong>...
</strong></code></pre>
{% endtab %}

{% tab title="200 OK respone" %}
{% code overflow="wrap" %}
```json
{
  "offers": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/offers",
    "offer": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709",
        "name": "Home Page Security & Backup Recovery Features",
        "trigger": "Always Triggered",
        "productOffers": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers"
        },
        "categoryOffers": {},
        "offerBundleGroups": {}
      }
    ],
    "totalResults": 1,
    "totalResultPages": 1
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting all products for the offer

You can get all products for an offer by submitting a [`GET /shoppers/me/offers/{offerId}/product-offers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1offers\~1%7BofferId%7D\~1product-offers/get) request. A successful request returns a `200 OK response`.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/offers/{offerId}/product-offers' \
<strong>--header 'Authorization: Bearer &#x3C;API_key>' \
</strong><strong>...
</strong></code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "productOffers": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers",
    "productOffer": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/offers/154344709/product-offers/64358400",
        "id": 64358400,
        "product": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358400",
          "displayName": "Class III",
          "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIIIThumb_v2.jpg"
        },
        "pricing": {
          "listPrice": {
            "currency": "USD",
            "value": "19.99"
          },
          "salePriceWithQuantity": {
            "currency": "USD",
            "value": "19.99"
          },
          "formattedListPrice": "$39.99",
          "formattedSalePriceWithQuantity": "$38.99",
          "listPriceIncludesTax": "false"
        }
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
