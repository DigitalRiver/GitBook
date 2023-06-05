---
description: >-
  Learn how to retrieve all point of promotion (POP) offers for a specific
  product.
---

# Retrieving all point of promotion offers for a specific product

You can retrieve all point of promotion (POP) offers for a specific [product identifier](../../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`) by submitting a [`GET`\
`/v1/shoppers/me/products/{productId}/point-of-promotions/{popName}/offers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1point-of-promotions\~1%7BpopName%7D\~1offers/get) request. A successful request returns a `200 OK response`.

The retrieved offers include the following:

* All always-triggered offers
* All promotional URLs and externally triggered offers, even if an offer is not triggered&#x20;
* All coupon code offers, even if an offer is not triggered&#x20;

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/point-of-promotions/{popName}/offers' \
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
