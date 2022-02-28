---
description: Learn how to get line items from a cart.
---

# Getting line items from a cart

## Get line items from a cart

You can use the [Line Items](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Line-Items) resource to get all line items, including products, pricing, and tax information from a cart.

{% tabs %}
{% tab title="URI" %}
```http
GET /v1/shoppers/me/carts/active/line-items
```
{% endtab %}

{% tab title="Request header" %}
```http
Host: api.digitalriver.com
Accept: application/json
Authorization: bearer your_access_token
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_102)
```
{% endtab %}

{% tab title="Request body" %}
```
The request body should be empty.
```
{% endtab %}

{% tab title="Response header" %}
```http
HTTP/1.1 200 OK
```
{% endtab %}

{% tab title="Response body" %}
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

## Line item

The `lineItems` in the cart's response body provide the details of a physical or digital product including, quantity, product, product ID, pricing.

### Product

A `product` provides the details of a physical or digital product.

### Pricing

The `pricing` defines the pricing for the item and provides the tax information. Digital River provides the tax rate (`taxRate`) information and the amount (`tax`) at the line item level.

### Tax

Digital River automatically calculates the tax rate. The `taxRate` requires a decimal value. For example, if the calculated tax rate is 19%, the value is `.19`, as shown in the following example.

{% tabs %}
{% tab title="Example" %}
```javascript
"tax": {
	"currency": "EUR",
	"value": 6.93
},
"taxRate": 0.19
```
{% endtab %}
{% endtabs %}

