---
description: Learn how to apply an offer.
---

# Applying an offer

You can apply an offer to a cart by including the applied product offers ([`appliedProductOffers`](https://drapi.io/commerce/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post)) object in the payload.

{% code title="Request example" %}
```html
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active?expand=all' \
--header 'Accept: application/json' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: applicati0n/json'
```
{% endcode %}

{% code title="Payload example" %}
```json
{
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
}

```
{% endcode %}

&#x20;
