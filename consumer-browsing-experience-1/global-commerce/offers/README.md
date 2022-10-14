---
description: Understand how offers work.
---

# Offers

An _offer_ is a promotion or discount intended to entice customers to purchase from a store. A product offer promotes a product within an offer and provides the information to feature or discount a product within an offer. The following table describes the available offer types:

| Offer type             | Definition                                                                                                                                                                                                                                 | Example of use                                                                                   | Does offer have a parent product? | Requires an API call? | Resource                                                                                                                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | --------------------------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| All Products Bundle    | A bundle offer that provides a free or discounted product when any product is purchased.                                                                                                                                                   | “Buy any product and get a free pen.”                                                            |                                   |                       |                                                                                                                                                                                                           |
| Banner                 | Promotes a product through a banner image on your store, in a shopping cart, and so on.                                                                                                                                                    | Advertise new product lines with a banner ad.                                                    | No                                | Yes                   | [Shopper](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)                                                                                                                         |
| Bundle                 | A bundle offer that adds a specific product to the shopping cart when another product is added to the shopping cart by the customer.                                                                                                       | “Buy a DVD player and automatically get a free universal remote.”                                |                                   |                       |                                                                                                                                                                                                           |
| Buy M, Get N           | A bundle offer that presents a free or discounted product when another product is purchased.                                                                                                                                               | “Buy one, get one free!”                                                                         |                                   |                       |                                                                                                                                                                                                           |
| Candy rack             | A promotion that appears in the shopping cart as a line item. The customer can add the item to their shopping cart by clicking the “Add” button.                                                                                           |                                                                                                  | Yes                               | Yes                   | [Cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)                                                                                                                       |
| Cross-sell             | Presents the customer with an additional product (or products) when they add a specific product to their shopping cart.                                                                                                                    | Offer the customer accessories for the digital camera they just added to the shopping cart.      | Yes                               | Yes                   | <p><a href="https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper">Cart</a></p><p><a href="https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products">Products</a></p> |
| Discount               | Provides a discount for a specific product, a set of products, a category of products, or all products in your store.                                                                                                                      | Create a discount for products in your store.                                                    |                                   |                       |                                                                                                                                                                                                           |
| Featured products      | Shows a list of “featured” products somewhere on your store (typically the home page). There is technically no limit to the number of products you can include but we recommend you limit your featured products to five products or less. | “This month’s special deals.”                                                                    | No                                | Yes                   | [Shopper](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)                                                                                                                         |
| Shopper-Defined Bundle | This bundle offer presents a list of products from which the customer can create their bundle.                                                                                                                                             | “Choose any 3 products for $9.99.”                                                               |                                   |                       |                                                                                                                                                                                                           |
| Up-sell                | Presents the customer with an alternate product (or products) when they add a specific product to their shopping cart.                                                                                                                     | Offer the customer a “gold” edition when they add the “standard” edition to their shopping cart. | Yes                               | Yes                   | <p><a href="https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper">Cart</a></p><p><a href="https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products">Products</a></p> |

Offers use a POP (Point-of-Promotion) to visually display the offer. A POP determines where an offer appears in an online store. A POP can be an interstitial page, banner or home page image, pop-up window, and so forth. Offer behavior is based on the offer configuration in Global Commerce. In the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource, offers retrieved for a cart must be POP-driven. Providing a POP when getting offers for a customer or product is now optional.

The following offers are automatically applied and do not require API calls as products are added to a cart:

* Certain offers without POPs, such as shipping offers
* Discounts
* Bundles.
* Buy M, Get N

You cannot use the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource to retrieve coupon-related offers; however, you can [apply a coupon or promo coupon offers to a cart](../#apply-coupon-code-to-a-cart) using the `POST shoppers/me/carts/active` resource method in the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource. Updating the cart applies the coupon discount. If desired, you can get a coupon offer that was applied to a cart.

The Offers resource returns the configured attributes for an offer. The product offer contains offer-specific information about the product, including the offer-specific price of the product. You can apply both the Offers resource and the [Product Offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Product-Offers) resource to a product, cart, or customer. Feature product offers such as a banner are specific to a shopper, shipping offers and candy rack offers are specific to a cart, and bundled parent-child product offers are specific to a product, for instance.

To retrieve all available offers for a customer, product, or cart resource respectively, use the following APIs:

* `GET shoppers/me/point-of-promotions/{popName}/offers`
* `GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers`
* `GET shoppers/me/carts/active/point-of-promotions/{popName}/offers`

The `popName` and ID originates in Global Commerce.

Offers are applied to a cart—offers are not applied to a customer. The API applies offers to the line-items within a cart. Coupon code limits may apply to a customer if a coupon code offer has been configured in Global Commerce to limit the code to one per customer.

When multiple offers are configured for a product, the offer that provides the greatest discount (the lowest price) for an order takes precedence. Also, a line-item can have an order discount applied in conjunction with a product discount. For more information about configuring offers and offer precedence, refer to the online help in the Global Commerce (also known as the Digital River Command Console).

Shipping offers that meet the offer criteria are applied automatically by the Global Commerce engine as products are added to a cart and do not require API calls. Discounts, bundles, and "buy x, get y" offers are applied automatically as well.