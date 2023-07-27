---
description: Understand the warnings object.
---

# Warnings object

A warning is triggered when there is a problem applying a valid coupon code to a cart. For example, a shopper uses a product-restricted line item coupon code when the product is not in a cart or a shipping offer coupon code when the shipping method is unavailable for the cart or country.

A `warnings` object should contain the following details: the code and description associated with the warning in a `200 OK` response.

The Shopper APIs use the following format for warnings:

{% code overflow="wrap" %}
```json
"Warnings": [
    {
      "Code": "couponcode_not_eligible",
      "description": "The relevant discount triggered by {coupon code} will be applied to the cart once it meets the offer criteria."
    }
  ]
```
{% endcode %}