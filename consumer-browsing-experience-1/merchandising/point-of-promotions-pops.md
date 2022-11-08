---
description: Understand how to use POPs.
---

# Point of promotions (POPs)

Offers use a POP to display the offer. A POP determines where an offer appears in an online store. A POP can be an interstitial page, banner or homepage image, pop-up window, and so forth. You can configure the offer's POP when you configure the offer in Global Commerce. Offers retrieved for a cart using the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource must be POP-driven. Providing a POP when getting offers for a shopper or products is now optional. The system automatically applies the following offers to a cart:

* Certain offers without POPs, such as shipping offers
* Discounts
* Bundles.
* Buy M, Get N

![](<../../.gitbook/assets/Digital\_River\_Demo\_Online\_Store\_Checkout (1).png>)

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
GET /shoppers/me/point-of-promotions/Home_topSeller/offers
```
{% endcode %}
{% endtab %}

{% tab title="Request header" %}
{% code overflow="wrap" %}
```http
Host: api.digitalriver.com
User-Agent: API Client/1.0
Accept: */*
Authorization: bearer your_access_token
```
{% endcode %}
{% endtab %}

{% tab title="Payload" %}
```
The request body should be empty.
```
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
	"offers": {
		"offer": [
			{
				"name": "Home_topSeller_1",
				"productOffers": {
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID/product-offers"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID"
			},
			{
				"name": "Home_topSeller_2",
				"productOffers": {
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID/product-offers"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID"
			},
			{
				"name": "Home_topSeller_3",
				"productOffers": {
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID/product-offers"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID"
			},
			{
				"name": "Home_topSeller_4",
				"productOffers": {
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID/product-offers"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers/offer_ID"
			}
		],
		"_uri": "https://api.digitalriver.com/v1/shoppers/me/point-of-promotions/Home_topSeller/offers"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

You do not need to send additional API calls to get these offers when a shopper adds products to a cart.

You cannot use the [Offers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Offers)resource to retrieve coupon-related offers. However, you can apply a coupon or promo coupon offers to a cart using the POST shoppers/me/carts/active resource method in the Carts API. Updating the cart applies the coupon discount. If desired, you can get the coupon offer that the shopper applied to a cart.

The Offers resource returns the configured attributes for an offer. The product offer contains offer-specific information on the product, including the offer-specific price of the product. You can apply both the Offers resource and the [Product Offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Product-Offers) resource to a product, cart, or shopper. Feature product offers such as a banner are specific to a shopper. Shipping offers and candy rack offers are specific to a cart, and bundled parent-child product offers are specific to a product, for instance.

To retrieve all available offers for a shopper, product, or cart resource respectively, use the following resources:

* GET shoppers/me/point-of-promotions/{popName}/offers
* GET shoppers/me/products/{productId}/point-of-promotions/{popName}/offers
* GET shoppers/me/carts/active/point-of-promotions/{popName}/offers

The `popName` and ID originates in Digital River.

The system applies offers to a cart—it does not apply offers to a shopper. The API applies offers to the line items within a cart. Coupon code limits may apply to a shopper if you configure a coupon code offer in Digital River to limit the code to one per shopper.

When you configure multiple offers for a product, the offer that provides the greatest discount (the lowest price) for an order takes precedence. Also, a line item can have an order discount applied in conjunction with a product discount. For more information on configuring offers and offer precedence, refer to the online help in Global Commerce.

Global Commerce applies shipping offers automatically to products added to a cart when they meet the offer criteria and do not require API calls. Global Commerce also automatically applies discounts, bundles, and "buy x, get y" offers.
