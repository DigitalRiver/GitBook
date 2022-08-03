---
description: Learn how to add a product to a cart.
---

# Adding a product to a cart

To add a product to a cart, provide the product identifier ([`productId`](https://drapi.io/commerce/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post)) and the term identifier ([`termId`](https://drapi.io/commerce/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post)) in the request.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/shoppers/me/carts/active?productId={pid}&termId={termId}' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endtab %}
{% endtabs %}

A successful request returns a `200 OK` response.

{% tabs %}
{% tab title="200 OK response" %}
```javascript
{
	"cart": {
		"id": "13871346482",
		"webCheckout": {
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/web-checkout"
		},
		"lineItems": {
			"lineItem": {
				"id": "line_item_ID",
				"quantity": "1",
				"product": {
					"displayName": "Network Pro",
					"thumbnailImage": "http://.../Storefront/Company/aqued/images/product/thumbnail/80x80net.png",
					"_uri": "https://api.digitalriver.com/v1/shoppers/me/products/product_ID"
				},
				"pricing": {
					"listPrice": {
						"_currency": "USD",
						"__text": "2.00"
					},
					"listPriceWithQuantity": {
						"_currency": "USD",
						"__text": "2.00"
					},
					"salePriceWithQuantity": {
						"_currency": "USD",
						"__text": "1.80"
					},
					"formattedListPrice": "$2.00",
					"formattedListPriceWithQuantity": "$2.00",
					"formattedSalePriceWithQuantity": "$1.80"
				},
				"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/line_item_ID"
			},
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items"
		},
		"totalItemsInCart": "1",
		"billingAddress": {
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
		},
		"shippingAddress": {
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
		},
		"payment": "",
		"shippingMethod": "",
		"shippingOptions": {
			"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options"
		},
		"pricing": {
			"subtotal": {
				"_currency": "USD",
				"__text": "1.80"
			},
			"discount": {
				"_currency": "USD",
				"__text": "0.18"
			},
			"shippingAndHandling": {
				"_currency": "USD",
				"__text": "0.00"
			},
			"tax": {
				"_currency": "USD",
				"__text": "0.00"
			},
			"orderTotal": {
				"_currency": "USD",
				"__text": "1.62"
			},
			"formattedSubtotal": "$1.80",
			"formattedDiscount": "$0.18",
			"formattedShippingAndHandling": "$0.00",
			"formattedTax": "$0.00",
			"formattedOrderTotal": "$1.62"			
		},
      "tax": {
        "currency": "USD",
        "value": 2.00
      },		
      "taxRate": 0.1111           
		"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active"
	}
}
```
{% endtab %}
{% endtabs %}

<mark style="background-color:orange;"></mark>
