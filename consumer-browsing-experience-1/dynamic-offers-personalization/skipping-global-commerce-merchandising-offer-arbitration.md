---
description: Learn how to bypass offer arbitration.
---

# Skipping Global Commerce merchandising offer arbitration

This feature allows you to bypass offer arbitration in a cart by triggering a promotional URL offer using a Shopper API.

{% hint style="info" %}
**Note**: The client can optionally include a flag in the Commerce API call when adding products to the cart, or relevant API resources to skip the Global Commerce Merchandising offer arbitration for the entire cart. When the flag is not present, the offer arbitration should perform as usual.
{% endhint %}

## High-level workflow

1. The user calls the Cart or Purchase resource with the offer ID (parent-child relationship type offer) and skips the Global Commerce Merchandising offer (the flag is enabled).
2. Digital River validates and determines the list price for the product.
3. The shopper can see the correct discount applied in the cart.
4. The system applies the shopper's default address to the cart.
5. The system applies the default payment option to the cart.
6. The shopper submits the cart.
7. The system creates an order.
