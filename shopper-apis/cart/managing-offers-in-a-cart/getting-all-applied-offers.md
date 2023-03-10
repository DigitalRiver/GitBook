---
description: Learn how to retrieve all offers applied to the cart.
---

# Getting all applied offers

An applied offer is the best eligible offer that is applied to the customer's cart. By best, we mean this offer won [offer arbitration](reconciling-conflicting-offers.md#offer-arbitration). Note that there could be a [winner for each discount level](reconciling-conflicting-offers.md#arbitration-by-discount-level).

You can [retrieve all offers applied to a customer's cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers/get).&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/applied-offers' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "appliedOffers": [
    {
      "id": "19383398500",
      "cartDescription": "Description of the cart",
      "appliedCouponCode": "CouponCodeExample",
      "appliedTo": {
        "appliedLevel": "Product(s) (Line Item)",
        "cartId": "33478770190",
        "lineItemId": "15217540193"
      },
      "type": "Discount"
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
