---
description: Understand how to use offers.
---

# Offers

An offer is a discount promotion that entices shoppers to purchase a product from your store. Most offers provide a discount on the price of a product or shipping costs. You can create an offer that promotes certain products or encourages shoppers to purchase additional products. See [Offer types](offers.md#offer-types) for more information.

The following image shows an example of how you can display a discount on a category list page.

![](<../../../.gitbook/assets/discount (1).png>)

## Offer types

The following table describes the available offer types:

| Offer Type             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| All Products Bundle    | <p>A bundle offer that provides a free or discounted product when a shopper purchases any product.</p><p><strong>Example</strong>: “Buy any product and get a free pen.”</p>                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Banner                 | <p>Promotes a product through a banner image in your store, in a shopping cart, and so on.</p><p><strong>Example</strong>: Advertise new product lines with a banner ad.</p><p><strong>Offer resource method</strong>:</p><p><code>GET shoppers/me/point-of-promotions/(popName)/offers</code></p><p><strong>Does the offer have a parent product</strong>? No</p><p><strong>Requires an API call</strong>? Yes</p>                                                                                                                                                                                                  |
| Bundle                 | <p>A bundle offer that adds a specific product to the shopping cart when a shopper adds another product to the shopping cart.</p><p><strong>Example</strong>: “Buy a DVD player and automatically get a free universal remote.”</p>                                                                                                                                                                                                                                                                                                                                                                                  |
| Buy M, Get N           | <p>A bundle offer that presents a free or discounted product when a shopper purchases another product.</p><p><strong>Example</strong>: “Buy one, get one free!”</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Candy rack             | <p>A promotion that appears in the shopping cart as a line item. The shopper can add the item to their shopping cart by clicking the add button.</p><p><strong>Best Practices</strong>: Use the Cross-Sell offer type when you create an offer for this POP.</p><p><strong>Offer resource method</strong>:</p><p><code>GET shoppers/me/carts/active/point-of-promotions/{popName}/offers</code></p><p><strong>Does the offer have a parent product</strong>? Yes</p><p><strong>Requires an API call</strong>? No</p>                                                                                                 |
| Cross-sell             | <p>Presents the shopper with one or more products when they add a specific product to their shopping cart.</p><p><strong>Example</strong>: When a shopper adds a digital camera to their shopping cart, offer the shopper accessories for the digital camera.</p><p><strong>Offer resource methods</strong>:</p><p><code>GET shoppers/me/carts/active/point-of-promotions/{popName}/offers</code></p><p><code>GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers</code></p><p><strong>Does the offer have a parent product</strong>? Yes</p><p><strong>Requires an API call</strong>? Yes</p> |
| Discount               | <p>The offer provides a discount for a specific product, a set of products, a category of products, or all products in your store.</p><p><strong>Example</strong>: Create a discount for products in your store.</p>                                                                                                                                                                                                                                                                                                                                                                                                 |
| Featured products      | <p>Shows a list of “featured” products somewhere in your store (typically the home page). You can include any number of products.</p><p><strong>Best Practices</strong>: Limit your featured products to five products or less.</p><p><strong>Example</strong>: “This month’s special deals.”</p><p><strong>Offer resource method</strong>:</p><p><code>GET shoppers/me/point-of-promotions/(popName)/offers</code></p><p><strong>Does the offer have a parent product</strong>? No</p><p><strong>Requires an API call</strong>? Yes</p>                                                                             |
| Shopper-Defined Bundle | <p>A bundle offer presents a list of products from which the shopper can create their bundle.</p><p><strong>Example</strong>: “Choose any 3 products for $9.99.”</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Up-sell                | <p>Presents the shopper with an alternate product (or products) when they add a specific product to their shopping cart.</p><p><strong>Example</strong>: Offer the shopper a “gold” edition when they add the “standard” edition to their shopping cart.</p><p><strong>Offer resource method</strong>:</p><p><code>GET shoppers/me/carts/active/point-of-promotions/{popName}/offers</code></p><p><code>GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers</code></p><p><strong>Does the offer have a parent product</strong>? Yes</p><p><strong>Requires an API call</strong>? Yes</p>       |