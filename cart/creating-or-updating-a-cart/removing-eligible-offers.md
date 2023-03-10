---
description: Learn how to remove eligible offers from a customer's cart
---

# Removing eligible offers

An eligible offer appears in the cart when the cart meets the requirement. There may be several offers of the same type (for example, always trigger percentage discount) available for the cart. The [offer arbitration](reconciling-conflicting-offers.md#offer-arbitration) will only apply the best offer to ensure the best discount for the customer.

For example, a customer's cart contains two offers: free shipping and 20% off for a single line item. These offers are available at the site level, so the discount is available to every shopper. You want to give a shopper a special 10% discount for each line item (line item A and line item B). In this instance, you can [delete all offers from the cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1eligible-offers/delete) and [replace them with a 10% discount for each line item](applying-an-offer.md).

When you [delete all eligible offers from a customer's cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Cart-Offers/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1eligible-offers/delete), the request resets the cart's promotions and clears all discounts and offers, including:

* Always trigger offers (site level)
* Promotional URLs or external trigger offers (user level)
* Coupon codes (user level)
* Bundle offers, all product bundle offers, cross-sell offers, and custom bundle offers

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request DELETE ' https://api.digitalriver.com/v1/shoppers/me/carts/active/eligible-offers' \
--header 'Accept: application/json' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: applicati0n/json'
```
{% endcode %}
{% endtab %}
{% endtabs %}
