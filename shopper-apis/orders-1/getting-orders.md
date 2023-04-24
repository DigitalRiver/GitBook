---
description: Learn how to retrieve orders.
---

# Getting orders

## Getting all orders

You can [get all orders for a shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders/get).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders?expand=all&pageSize=1' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/orders",
  "order": [
    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47276010023",
      "id": "47276010023",
      "submissionDate": "2018-04-27T18:01:01.000Z",
      "displayName": "New Order",
      "locale": "en_US",
      "optIn": "false",
      "testOrder": "false",
      "taxExempt": "false",
      "businessEntityCode": "DR_INC-ENTITY",
      "pricing": {
        "subtotal": {
          "currency": "USD",
          "value": "19.99"
        },
        "subtotalWithDiscount": {
          "currency": "USD",
          "value": "19.99"
        },
        "incentive": {
          "currency": "USD",
          "value": "19.99"
        },
        "shipping": {
          "currency": "USD",
          "value": "19.99"
        },
        "tax": {
          "currency": "USD",
          "value": "19.99"
        },
        "total": {
          "currency": "USD",
          "value": "19.99"
        },
        "formattedSubtotal": "$17.99",
        "formattedSubtotalWithDiscount": "$12.99",
        "formattedIncentive": "$5.00",
        "formattedShipping": "$0.00",
        "formattedTax": "$0.96",
        "formattedTotal": "$13.95"
      },
      "payment": {
        "paymentMethodName": "discover",
        "displayableNumber": "************4321",
        "expirationMonth": "01",
        "expirationYear": "2020",
        "customerFirstName": "AUTOMATION",
        "customerLastName": "TESTER",
        "customerEmail": "automatedtester68091904@digitalriver.com",
        "paymentAmount": {
          "currency": "USD",
          "value": "19.99"
        },
        "softDescriptor": "DRI*demosft1"
      },
      "orderState": "Complete",
      "orderStateDetails": {
        "description": "Not Settled",
        "settled": {
          "currency": "USD",
          "value": "19.99"
        },
        "refunded": {
          "currency": "USD",
          "value": "19.99"
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
      "lineItems": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278020023/line-items",
        "lineItem": [
          {
            "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278020023/line-items/488822310023",
            "id": "488822310023",
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
            "lineItemState": "Complete",
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
              "formattedListPrice": "$19.99",
              "formattedListPriceWithQuantity": "$19.99",
              "formattedSalePrice": "$17.99",
              "formattedSalePriceWithQuantity": "$17.99",
              "totalDiscountWithQuantity": {
                "currency": "USD",
                "value": "19.99"
              },
      				"tax": {
      				"vatPercentage": 0
      				"currency": "USD",
      				"value": 2.00
      				},
      				"taxRate": 0.1111          
      				},			  
              "formattedTotalDiscountWithQuantity": "$2.00",
              "discountDescription": "10%"
            },
            "downloads": {
              "downloadUri": "http://wgtintot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D3E56B5723F9D46513279A35381E6ECCFA38DC305C96D769173E906E98A04A2B5BBA82B10B42A63223B365B18617EBAE466D6993DA22958AFE291C52E8142F3D62B9F021B53460271F0451C577DBEF2976/demosft1/WaterLilies.jpg"
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
        ]
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
  ],
  "totalResults": "1",
  "totalResultPages": "1"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [`Order query parameters`](../../general-resources/shopper-apis-reference/orders.md#orders-query-parameters) for more information.

## Getting an order by ID

To [retrieve an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D/get), you must specify the order identifier (`orderId`). You can optionally include the state of the order. Possible order states are `Open`, `Submitted`, `Cancelled`, `Complete`, `Pending Payment`, `In Review`, and `In Process`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/orders/9999999999' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47276010023",
  "id": "47276010023",
  "submissionDate": "2018-04-27T18:01:01.000Z",
  "displayName": "New Order",
  "locale": "en_US",
  "optIn": "false",
  "testOrder": "false",
  "taxExempt": "false",
  "businessEntityCode": "DR_INC-ENTITY",
  "pricing": {
    "subtotal": {
      "currency": "USD",
      "value": "19.99"
    },
    "subtotalWithDiscount": {
      "currency": "USD",
      "value": "19.99"
    },
    "incentive": {
      "currency": "USD",
      "value": "19.99"
    },
    "shipping": {
      "currency": "USD",
      "value": "19.99"
    },
    "tax": {
      "currency": "USD",
      "value": "19.99"
    },
    "total": {
      "currency": "USD",
      "value": "19.99"
    },
    "formattedSubtotal": "$17.99",
    "formattedSubtotalWithDiscount": "$12.99",
    "formattedIncentive": "$5.00",
    "formattedShipping": "$0.00",
    "formattedTax": "$0.96",
    "formattedTotal": "$13.95"
  },
  "payment": {
    "paymentMethodName": "discover",
    "displayableNumber": "************4321",
    "expirationMonth": "01",
    "expirationYear": "2020",
    "customerFirstName": "AUTOMATION",
    "customerLastName": "TESTER",
    "customerEmail": "automatedtester68091904@digitalriver.com",
    "paymentAmount": {
      "currency": "USD",
      "value": "19.99"
    },
    "softDescriptor": "DRI*demosft1"
  },
  "orderState": "Complete",
  "orderStateDetails": {
    "description": "Not Settled",
    "settled": {
      "currency": "USD",
      "value": "19.99"
    },
    "refunded": {
      "currency": "USD",
      "value": "19.99"
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
  "lineItems": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278020023/line-items",
    "lineItem": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47278020023/line-items/488822310023",
        "id": "488822310023",
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
        "lineItemState": "Complete",
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
          "formattedListPrice": "$19.99",
          "formattedListPriceWithQuantity": "$19.99",
          "formattedSalePrice": "$17.99",
          "formattedSalePriceWithQuantity": "$17.99",
          "totalDiscountWithQuantity": {
            "currency": "USD",
            "value": "19.99"
          },
		  "tax": {
			"vatPercentage": 0
			"currency": "USD",
			"value": 2.00
			},
			"taxRate": 0.1111          
		  },
        "discountDescription": "string",
        "msrpPrice": {
          "value": 0,
          "formattedValue": "string"
        },		  
          "formattedTotalDiscountWithQuantity": "$2.00",
          "discountDescription": "10%"
        },
        "downloads": {
          "downloadUri": "http://wgtintot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D3E56B5723F9D46513279A35381E6ECCFA38DC305C96D769173E906E98A04A2B5BBA82B10B42A63223B365B18617EBAE466D6993DA22958AFE291C52E8142F3D62B9F021B53460271F0451C577DBEF2976/demosft1/WaterLilies.jpg"
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
    ]
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
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [`Order query parameters`](../../general-resources/shopper-apis-reference/orders.md#orders-query-parameters) for more information.
