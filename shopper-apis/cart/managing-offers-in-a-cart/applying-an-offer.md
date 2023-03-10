---
description: Learn how to apply an offer.
---

# Applying an offer

Use [`POST /v1/shoppers/me/carts/active?expand=all`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) to apply an offer to a cart by including the applied product offers ([`appliedProductOffers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post)) object in the payload.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active?expand=all' \
--header 'Authorization: bearer {{access_token}}' \
...
--data-raw '{
  "cart": {
    "lineItems": {
      "lineItem": [
        {
          "quantity": 1,
          "product": {
            "id": 5181808200
          }
        }
      ],
      "appliedProductOffers": {
        "offer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        },
        "shippingOffer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        }
      }
    },
    "appliedOrderOffers": {
      "offer": {
        "offerId": "100029992",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      },
      "shippingOffer": {
        "offerId": "123111333",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      }
    }
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 OK` response.
