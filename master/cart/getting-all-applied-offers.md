---
description: Learn how to retrieve all offers applied to the cart.
---

# Getting all applied offers

An applied offer is the best eligible offer that is applied to the customer's cart. By best, we mean this offer won offer arbitration. Note that there could be a [winner for each discount level](reconciling-conflicting-offers.md#arbitration-by-discount-level).

You can [retrieve all offers applied to a customer's cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get).&#x20;

{% code title="Request example" overflow="wrap" %}
```html
curl --location -g --request DELETE ' https://api.digitalriver.com/v1/shoppers/me/carts/active/applied-offers' \
--header 'Accept: application/json' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: applicati0n/json'
```
{% endcode %}
