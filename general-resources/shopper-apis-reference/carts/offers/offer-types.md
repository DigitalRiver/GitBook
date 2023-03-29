---
description: Understand the available offer types.
---

# Offer types

The following topics describe the available offer types.

## All products bundle

A bundle offer that provides a free or discounted product when a shopper purchases any product.

**Example**: “Buy any product and get a free pen.”

## Banner

Promotes a product through a banner image in your store, in a shopping cart, and so on.

**Example**: Advertise new product lines with a banner ad.

**Offer resource method**: `GET shoppers/me/point-of-promotions/(popName)/offers`

**Does the offer have a parent product**? No

**Requires an API call**? Yes

## Bundle

A bundle offer adds a specific product to the shopping cart when a shopper adds another product to the shopping cart.

**Example**: “Buy a DVD player and automatically get a free universal remote.”

## Buy M, Get N

A bundle offer that presents a free or discounted product when a shopper purchases another product.

**Example**: “Buy one, get one free!”

## Candy rack

A promotion that appears in the shopping cart as a line item. The shopper can add the item to their shopping cart by clicking the add button.

**Best Practices**: Use the Cross-Sell offer type when you create an offer for this POP.

**Offer resource method**:

`GET shoppers/me/carts/active/point-of-promotions/{popName}/offers`

**Does the offer have a parent product**? Yes

**Requires an API call**? No

## Cross-sell

Presents the shopper with one or more products when they add a specific product to their shopping cart.

**Example**: When a shopper adds a digital camera to their shopping cart, offer the shopper accessories for the digital camera.

**Offer resource methods**:

`GET shoppers/me/carts/active/point-of-promotions/{popName}/offers`

`GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers`

**Does the offer have a parent product**? Yes

**Requires an API call**? Yes

## Discount

The offer provides a discount for a specific product, a set of products, a category of products, or all products in your store.

**Example**: Create a discount for products in your store.

## Featured products

Shows a list of “featured” products somewhere in your store (typically the home page). You can include any number of products.

**Best Practices**: Limit your featured products to five products or less.

**Example**: “This month’s special deals.”

**Offer resource method**:

`GET shoppers/me/point-of-promotions/(popName)/offers`

**Does the offer have a parent product**? No

**Requires an API call**? Yes

## Shopper-Defined Bundle

A bundle offer presents a list of products from which the shopper can create their bundle.

**Example**: “Choose any 3 products for $9.99.”

## Up-sell

Presents the shopper with an alternate product (or products) when they add a specific product to their shopping cart.

**Example**: Offer the shopper a “gold” edition when they add the “standard” edition to their shopping cart.

**Offer resource method**:

`GET shoppers/me/carts/active/point-of-promotions/{popName}/offers`

`GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers`

**Does the offer have a parent product**? Yes

**Requires an API call**? Yes
