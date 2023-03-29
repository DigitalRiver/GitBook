---
description: Understand how offers work.
---

# Offers

An _offer_ is a promotion or discount intended to entice customers to purchase from a store. A product offer promotes a product within an offer and provides the information to feature or discount a product within an offer. The following table describes the available offer types:

Offers use a POP (Point-of-Promotion) to visually display the offer. A POP determines where an offer appears in an online store. A POP can be an interstitial page, banner or home page image, pop-up window, and so forth. Offer behavior is based on the offer configuration in Global Commerce. In the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource, offers retrieved for a cart must be POP-driven. Providing a POP when getting offers for a customer or product is now optional.

The following offers are automatically applied and do not require API calls as products are added to a cart:

* Certain offers without POPs, such as shipping offers
* Discounts
* Bundles
* Buy M, Get N

You cannot use the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource to retrieve coupon-related offers; however, you can [apply a coupon or promo coupon offers to a cart](../../../common-shoppers-and-admin-apis-reference/global-commerce/#apply-coupon-code-to-a-cart) using the `POST shoppers/me/carts/active` resource method in the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource. Updating the cart applies the coupon discount. If desired, you can get a coupon offer that was applied to a cart.

The Offers resource returns the configured attributes for an offer. The product offer contains offer-specific information about the product, including the offer-specific price of the product. You can apply both the Offers resource and the [Product Offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Product-Offers) resource to a product, cart, or customer. Feature product offers such as a banner are specific to a shopper, shipping offers and candy rack offers are specific to a cart, and bundled parent-child product offers are specific to a product, for instance.

To retrieve all available offers for a customer, product, or cart resource respectively, use the following APIs:

* `GET shoppers/me/point-of-promotions/{popName}/offers`
* `GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers`
* `GET shoppers/me/carts/active/point-of-promotions/{popName}/offers`

The `popName` and ID originates in Global Commerce.

Offers are applied to a cart—offers are not applied to a customer. The API applies offers to the line-items within a cart. Coupon code limits may apply to a customer if a coupon code offer has been configured in Global Commerce to limit the code to one per customer.

When multiple offers are configured for a product, the offer that provides the greatest discount (the lowest price) for an order takes precedence. Also, a line-item can have an order discount applied in conjunction with a product discount. For more information about configuring offers and offer precedence, refer to the online help in the Global Commerce (also known as the Digital River Command Console).

Shipping offers that meet the offer criteria are applied automatically by the Global Commerce engine as products are added to a cart and do not require API calls. Discounts, bundles, and "buy x, get y" offers are applied automatically as well.
