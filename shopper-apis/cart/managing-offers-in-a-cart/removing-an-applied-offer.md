---
description: Learn how to remove an offer applied to the cart.
---

# Removing an applied offer

You can [remove a specific offer applied to a customer's cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1applied-offers\~1%7BofferId%7D/delete).  If the offer type for the specified offer is bundle, the line item group will be broken up and the line item may be removed based on the bundle type.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request DELETE ' https://api.digitalriver.com/v1/shoppers/me/carts/active/applied-offers/{offerId}' \
--header 'Authorization: Basic {{access_token}}' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `204 Successful` response. See [Applied offers](../../../general-resources/shopper-apis-reference/carts/offers/applied-offers.md) for more information.
