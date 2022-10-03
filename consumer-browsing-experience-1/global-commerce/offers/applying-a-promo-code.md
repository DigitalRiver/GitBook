---
description: Learn how to apply a promo code.
---

# Applying a promo code

Send a `POST shoppers/me/carts/active` request to the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource with the required `promoCode` query parameter. The request must include a valid limited or full access token. There is no payload associated with this request; the request body is empty. The following request applies a promotional code value of `wb32xjtam`:

{% tabs %}
{% tab title="URI" %}
```http
POST https://api.digitalriver.com/v1/shoppers/me/carts/active?promoCode=wb32xjtam HTTP/1.1
```
{% endtab %}
{% endtabs %}

A successful request returns a status code of 200 in the response header; otherwise, error codes are returned in the response. The ID of the cart is `1234567890`.

{% tabs %}
{% tab title="The Cart object" %}
```javascript
{
	"cart": {
		"id": "1234567890",
		"lineitems": {
			"lineitem": {
				"id": "12765711619",
				"quantity": "1",
				"product": {
					"displayname": "Displayable Product Name",
					"thumbnailimage": "http://drh1.img.digitalriver.com/DRHM/Storefront/images/product/thumbnail/small-product-image.jpg",
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/products/232054400"
				},
				"pricing": {
					"listprice": {
						"_currency": "USD",
						"__text": "24.95"
					},
					"listpricewithquantity": {
						"_currency": "USD",
						"__text": "24.95"
					},
					"salepricewithquantity": {
						"_currency": "USD",
						"__text": "14.95"
					},
					"formattedlistprice": "$24.95",
					"formattedlistpricewithquantity": "$24.95",
					"formattedsalepricewithquantity": "$14.95"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/12765711619"
			},
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items"
		},
		"billingaddress": {
			"shippingaddress": {
				"payment": {
					"name": "Visa",
					"displayablenumber": "************1111",
					"expirationyear": "2017"
				},
				"shippingmethod": {
					"code": "142400",
					"description": "USPS - Priority Mail"
				},
				"shippingoptions": {
					"pricing": {
						"subtotal": {
							"_currency": "USD",
							"__text": "24.95"
						},
						"discount": {
							"_currency": "USD",
							"__text": "10.00"
						},
						"shippingandhandling": {
							"_currency": "USD",
							"__text": "0.00"
						},
						"tax": {
							"_currency": "USD",
							"__text": "0.00"
						},
						"ordertotal": {
							"_currency": "USD",
							"__text": "14.95"
						},
						"formattedsubtotal": "$24.95",
						"formatteddiscount": "$10.00",
						"formattedshippingandhandling": "$0.00",
						"formattedtax": "$0.00",
						"formattedordertotal": "$14.95"
					},
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/shipping-options"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
			},
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
		},
		"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active"
	 }
 }
```
{% endtab %}
{% endtabs %}

Typically, the next steps after applying a coupon code are submitting the cart and creating an order to complete the checkout process.
