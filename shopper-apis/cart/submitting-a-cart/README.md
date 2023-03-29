---
description: Learn how to submit a cart.
---

# Submitting a cart

Use the [Submit Cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Submit-Cart) resource to submit a cart. A cart cannot be submitted until the following items have been added or applied to the cart:

* One or more products
* Shipping option (if the product is a physical product)
* Shipping address
* Billing address
* Payment option

Submitting a cart creates the order. You can use the information in the response to build a Thank You page. If the customer purchased a digital product, the cart presents the download links to the customer. If the customer selects a check as the payment type, the cart provides delayed payment instructions. If the customer chooses a payment service provider as the payment type, the cart provides links to the payment provider such as PayPal.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'http://<<host>>/v1/shoppers/me/carts/active/submit-cart' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "order": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278080023",
    "id": "47278080023",
    "submissionDate": "2018-04-27T20:31:13.109Z",
    "displayName": "New Order",
    "locale": "en_US",
    "optIn": "false",
    "testOrder": "false",
    "taxExempt": "false",
    "businessEntityCode": "DR_INC-ENTITY",
    "orderState": "Submitted",
    "orderStateDetails": {
      "description": "Settled",
      "settled": {
        "currency": "USD",
        "value": "19.99"
      },
      "refunded": {
        "currency": "USD",
        "value": "19.99"
      }
    },
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
  "lineItems": {
    "lineItem": {
      "id": "488822390023",
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
      "lineItemState": "Downloadable",
      "lineItemStateDetails": {
        "description": "Downloadable - 1",
        "backOrdered": "0",
        "shipped": "0",
        "returned": "0",
        "pendingReturn": "0"
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
        "salePrice": {
          "currency": "USD",
          "value": "19.99"
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": "19.99"
        },
        "formattedListPrice": "$0.00",
        "formattedListPriceWithQuantity": "$0.00",
        "formattedSalePrice": "$0.00",
        "formattedSalePriceWithQuantity": "$0.00",
        "totalDiscountWithQuantity": {
          "currency": "USD",
          "value": "19.99"
        },
        "formattedTotalDiscountWithQuantity": "$0.00",
        "discountDescription": "string",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": "240.00"
        }
        "tax": {
          "currency": "USD",
          "value": 2.00
        },
        "taxRate": 0.1111        
      },
      "downloads": {
        "downloadUri": "http://wgtintot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D3E56B5723F9D46513279A35381E6ECCFA38DC305C96D769173E906E98A04A2B5B3CFFB85C93D810E7B365B18617EBAE4682F5E46FAD1C55CE291C52E8142F3D624C7461A8833978160451C577DBEF2976/demosft1/WaterLilies.jpg"
      },
      "customAttributes": {
        "attribute": [
          {
            "name": "name",
            "value": "string",
            "type": "string"
          }
        ]
      }
    }
  },
  "billingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
    "id": "billingAddress",
    "firstName": "Automation",
    "lastName": "Tester",
    "line1": "PO BOX 6930",
    "line2": "123",
    "line3": "Suite Line 3",
    "city": "Waconia",
    "countrySubdivision": "MN",
    "postalCode": 5387,
    "country": "US",
    "countryName": "United States",
    "phoneNumber": "099-222-44454",
    "emailAddress": "automatedTester68091904@digitalriver.com"
  },
  "shippingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
    "id": "billingAddress",
    "firstName": "Automation",
    "lastName": "Tester",
    "line1": "PO BOX 6930",
    "line2": "123",
    "line3": "Suite Line 3",
    "city": "Waconia",
    "countrySubdivision": "MN",
    "postalCode": 5387,
    "country": "US",
    "countryName": "United States",
    "phoneNumber": "099-222-44454",
    "emailAddress": "automatedTester68091904@digitalriver.com"
  },
  "pricing": {
    "subtotal": {
      "currency": "USD",
      "value": "19.99"
    },
    "subtotalWithDiscount": {
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
    "formattedSubtotal": "$0.00",
    "formattedSubtotalWithDiscount": "$0.00",
    "formattedDiscount": "$0.00",
    "formattedShippingAndHandling": "$0.00",
    "formattedTax": "$0.00",
    "formattedOrderTotal": "$0.00"
  },
  "payment": {}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Submit cart query parameters](../../../general-resources/shopper-apis-reference/submit-cart.md#submit-cart-query-parameters) for more information.
