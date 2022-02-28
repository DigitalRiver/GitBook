---
description: Learn how to create or update a cart.
---

# Creating or updating a cart

## Creating a cart

Use the `GET /shoppers/token` resource to create an anonymous (limited access) or authenticated (full access) token. The response to this request creates a shopping cart and returns an access token to be included in all other cart interactions.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request GET 'https://api.digitalriver.com/shoppers/me/carts/active' \
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
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active",
  "paymentMethods": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/payment-methods"
  },
  "applyPaymentMethod": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/apply-payment-method"
  },
  "submitCart": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/submit-cart"
  },
  "webCheckout": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/web-checkout"
  },
  "id": "47278010023",
  "lineItems": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items",
    "lineItem": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/488822300023",
      "id": "488822300023",
      "quantity": "1",
      "product": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "parentProduct": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
        },
        "id": "64578500",
        "name": "Class I",
        "displayName": "Class I",
        "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
        "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
        "productType": "DOWNLOAD",
        "sku": "Class I",
        "externalReferenceId": "Test External Reference Number",
        "companyId": "demosft1",
        "displayableProduct": "true",
        "purchasable": "true",
        "manufacturerName": "Test Manufacturer Name",
        "manufacturerPartNumber": "Test Manufacturer Part Number",
        "thumbnailImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "productImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
        "keywords": "testKeyword",
        "customAttributes": {
          "attribute": [
            {
              "name": "name",
              "value": "string",
              "type": "string"
            }
          ]
        }
      },
      "pricing": {
        "listPrice": {
          "currency": "USD",
          "value": "19.99"
        },
        "listPriceWithQuantity": {
          "currency": "USD",
          "value": "19.99"
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": "19.99"
        },
        "formattedListPrice": "$19.99",
        "formattedListPriceWithQuantity": "$19.99",
        "formattedSalePriceWithQuantity": "$17.99",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": 240.00
        },
        "tax": {
          "currency": "USD",
          "value": 2.00
        },
        "taxRate": 0.1111
      }
    }
  },
  "totalItemsInCart": "1",
  "businessEntityCode": "DR_INC-ENTITY",
  "billingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
  },
  "shippingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
  },
  "payment": {
    "name": "Discover",
    "displayableNumber": "************4321",
    "expirationMonth": "01",
    "expirationYear": "2020"
  },
  "shippingOptions": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options"
  },
  "pricing": {
    "subtotal": {
      "currency": "USD",
      "value": "19.99"
    },
    "discount": {
      "currency": "USD",
      "value": "19.99"
    },
    "shippingAndHandling": {
      "currency": "USD",
      "value": "19.99"
    },
    "tax": {
      "currency": "USD",
      "value": "19.99"
    },
    "orderTotal": {
      "currency": "USD",
      "value": "19.99"
    },
    "formattedSubtotal": "$17.99",
    "formattedDiscount": "$5.00",
    "formattedShippingAndHandling": "$0.00",
    "formattedTax": "$0.96",
    "formattedOrderTotal": "$13.95"
  }
}
```
{% endtab %}
{% endtabs %}

## Updating a cart

Use the [`POST /shoppers/me/carts/active`](https://drapi.io/commerce/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) resource to add products, coupon codes, billing/shipping addresses, and offers to a customer's cart.

All of the resources contained in the Cart can be leveraged to modify specific cart data elements.

{% hint style="danger" %}
**Required**: A level 3 API key, a legal/contract amendment, and PCI documentation are required to pass customer credit card information through the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource. Please reach out to your Account Manager if you are interested in this capability.
{% endhint %}

For example, to add a product to a cart:

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/shoppers/me/carts/active?productId=pid&termId=termId' \
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
