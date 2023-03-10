---
description: >-
  Learn how to resume cart submission after completing a redirect payment
  method.
---

# Resuming cart submission

When a customer selects a [redirect payment method](../../general-resources/reference/guidelines-for-capturing-payment-details.md#redirect-payment-methods) when they submit the cart, they are redirected to the payment provider where they can authorize the payment. Once the payment is authorized, you should resume submitting the cart.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request DELETE ' https://api.digitalriver.com/v1/shoppers/me/carts/active/resume-cart' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "resumeCart": {
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
          "backOrdered": 0,
          "shipped": 0,
          "returned": 0,
          "pendingReturn": 0
        },
        "pricing": {
          "listPrice": {
            "currency": "USD",
            "value": 101
          },
          "listPriceWithQuantity": {
            "currency": "USD",
            "value": 1010
          },
          "salePrice": {
            "currency": "USD",
            "value": 95.95
          },
          "salePriceWithQuantity": {
            "currency": "USD",
            "value": 959.5
          },
          "formattedListPrice": "101.00USD",
          "formattedListPriceWithQuantity": "1010.00USD",
          "formattedSalePrice": "95.95USD",
          "formattedSalePriceWithQuantity": "959.50USD",
          "totalDiscountWithQuantity": {
            "currency": "USD",
            "value": 50.5
          },
          "formattedTotalDiscountWithQuantity": "50.50USD",
          "formattedCommitmentPrice": "$240.00",
          "commitmentPrice": {
            "currency": "USD",
            "value": "240.00"
          },
          "productTax": {
            "currency": "USD",
            "value": "158.33"
          },
          "shippingTax": {
            "currency": "USD",
            "value": "1.91"
          },
          "feeTax": {
            "currency": "USD",
            "value": "18.25"
          },
          "taxRate": "0.1111",
          "discountDescription": "$10.00",
          "importTax": {
            "currency": "USD",
            "value": 0
          },
          "formattedImportTax": "0.00USD",
          "importDuty": {
            "currency": "USD",
            "value": 0
          },
          "formattedImportDuty": "0.00USD",
          "feePricing": {
            "fee": [
              {
                "name": "WEEE Fee",
                "typeCode": "typeCode",
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
                "formattedListPrice": "8.33USD",
                "formattedListPriceWithQuantity": "8.33USD",
                "formattedSalePriceWithQuantity": "8.33USD",
                "tax": {
                  "currency": "USD",
                  "value": "1.67"
                }
              }
            ]
          }
        },
        "downloads": {
          "downloadUri": "https://wgtintot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D3E56B5723F9D46513279A35381E6ECCFA38DC305C96D769173E906E98A04A2B5B3CFFB85C93D810E7B365B18617EBAE4682F5E46FAD1C55CE291C52E8142F3D624C7461A8833978160451C577DBEF2976/demosft1/WaterLilies.jpg"
        },
        "customAttributes": {
          "attribute": [
            {
              "name": "name",
              "value": "string",
              "type": "string"
            }
          ]
        },
        "billingAgreementId": "fc86a666-9f2f-4294-b591-468ae34122ff"
      }
    },
    "billingAddress": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
      "relation": "https://developers.digitalriver.com/v1/shoppers/AddressesResource",
      "id": "billingAddress",
      "firstName": "Automation",
      "lastName": "Tester",
      "companyName": "Digital River",
      "line1": "PO BOX 6930",
      "line2": "123",
      "line3": "Suite Line 3",
      "city": "Waconia",
      "countrySubdivision": "MN",
      "postalCode": "5387.0",
      "country": "US",
      "countryName": "United States",
      "phoneNumber": "099-222-44454",
      "emailAddress": "automatedTester@digitalriver.com",
      "countyName": "Hennepin",
      "phoneticFirstName": "クリス",
      "phoneticLastName": "ミラー",
      "division": "製品開発",
      "title": "M"
    },
    "shippingAddress": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
      "relation": "https://developers.digitalriver.com/v1/shoppers/AddressesResource",
      "id": "shippingAddress",
      "firstName": "Automation",
      "lastName": "Tester",
      "companyName": "Digital River",
      "line1": "PO BOX 6930",
      "line2": "123",
      "line3": "Suite Line 3",
      "city": "Waconia",
      "countrySubdivision": "MN",
      "postalCode": "5387.0",
      "country": "US",
      "countryName": "United States",
      "phoneNumber": "099-222-44454",
      "countyName": "Hennepin",
      "emailAddress": "automatedTester@digitalriver.com",
      "phoneticFirstName": "クリス",
      "phoneticLastName": "ミラー",
      "division": "製品開発"
    },
    "taxInclusive": false,
    "landedCostState": "NOT_ELIGIBLE",
    "pricing": {
      "subtotal": {
        "currency": "USD",
        "value": 1059.5
      },
      "subtotalWithDiscount": {
        "currency": "USD",
        "value": 1059.5
      },
      "discount": {
        "currency": "USD",
        "value": 0
      },
      "shippingAndHandling": {
        "currency": "USD",
        "value": 11.47
      },
      "importTaxAndDuty": {
        "currency": "USD",
        "value": 0
      },
      "tax": {
        "currency": "USD",
        "value": 178.49
      },
      "orderTotal": {
        "currency": "USD",
        "value": 1070.97
      },
      "formattedSubtotal": "1,059.50GBP",
      "formattedDiscount": "0.00USB",
      "formattedShippingAndHandling": "11.47USD",
      "formattedImportTaxAndDuty": "0.00USD",
      "formattedTax": "178.49USD",
      "formattedOrderTotal": "1,070.97USD"
    },
    "paymentMethod": {
      "type": "creditCard",
      "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
      "sourceClientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
      "creditCard": {
        "expirationYear": "2030",
        "lastFourDigits": "0000",
        "clientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
        "expirationMonth": "08",
        "fundingSource": "debit",
        "brand": "Visa",
        "reusable": "true"
      },
      "amountContributed": {
        "currency": "USD",
        "value": 1059.5
      },
      "charges": [
        {
          "chargeId": "1cac37c0-98a7-46b2-b9ed-fbc615c9f18a",
          "amount": {
            "currency": "USD",
            "value": 1059.5
          },
          "status": "failed",
          "createdTime": "2021-12-06T09:03:46.877Z",
          "updatedTime": "2021-12-06T09:03:46.877Z"
        }
      ],
      "supplementaryPaymentMethods": [
        {
          "type": "customerCredit",
          "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
          "sourceClientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
          "customerCredit": {
            "flow": "standard",
            "reusable": "true"
          },
          "charges": [
            {
              "chargeId": "cf57f9c9-8b0d-4e64-998a-816499fefa01",
              "amount": {
                "currency": "USD",
                "value": 1059.5
              },
              "status": "failed",
              "createdTime": "2021-12-06T09:03:46.877Z",
              "updatedTime": "2021-12-06T09:03:46.877Z"
            }
          ],
          "amountContributed": {
            "currency": "USD",
            "value": 1059.5
          }
        }
      ]
    },
    "payment": {
      "name": "Visa",
      "displayableNumber": "************1111",
      "expirationMonth": 0,
      "expirationYear": 2030,
      "softDescriptor": "DRI*demosft1"
    },
    "paymentCompletionResources": {},
    "termsOfSalesAcceptance": "true",
    "paymentSession": {
      "id": "string",
      "status": "string",
      "clientSecret": "string",
      "redirectUrl": "https://api.digitalriver.com:80/payments/redirects/12759bb0-xxxx-4bdb-bfeb-9095ba8059fc?apiKey=a88fxxxx1eef47eb95bc609c22e593c8"
    },
    "customerType": "B",
    "taxRegistrations": [
      {
        "key": "UK_VAT",
        "value": "GB698588737"
      }
    ],
    "organizationId": "digitalriver12345"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
