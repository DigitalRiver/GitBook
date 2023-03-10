---
description: Learn how to manage a web checkout.
---

# Managing web checkout

## Getting web checkout

The [`GET /web-checkout`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1web-checkout/get) request transfers the shopper to Digital River-hosted storefront pages. The response returns a `302 Found` with a location to the Digital River-hosted storefront pages.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/web-checkout' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Creating the cart and transferring the shopper

The [`POST /web-checkout`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1web-checkout/post) request creates the cart and transfers the shopper to the Digital River-hosted storefront pages. The response returns a `302 Found` with a location to the Digital River-hosted storefront pages.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/web-checkout' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "cart": {
    "lineItems": {
      "lineItem": {
        "quantity": "15",
        "product": {
          "id": "12345",
          "externalReferenceId": "12345",
          "companyId": "company"
        }
      }
    },
    "offers": {
      "offerId": "1234567890"
    }
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}
