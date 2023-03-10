---
description: Learn how to get all offers for a specific point of promotion (POP).
---

# Retrieving all offers for a specific point of promotion

You can retrieve all offers for a specific point of promotion (POP) by submitting a [`GET /shoppers/me/products/point-of-promotions/{popName}/offers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Offers/paths/\~1v1\~1shoppers\~1me\~1point-of-promotions\~1%7BpopName%7D\~1offers/get) request. A successful request returns a `200 OK response`.

The retrieved offers include:

* All always-triggered offers
* All promotional URLs and externally triggered offers, even if an offer is not triggered&#x20;

The retrieved offers do not include coupon code offers, even if a coupon code offer has been triggered.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 
'https://api.digitalriver.com/shoppers/me/point-of-promotions/{popName}/offers' \
<strong>--header 'Authorization: Bearer &#x3C;API_key>' \
</strong><strong>...
</strong></code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "offers": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/SiteMerchandising_HomePageStoreSpecials/offers",
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
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
