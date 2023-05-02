---
description: Learn how to apply an offer.
---

# Applying an offer

## Applying an offer to a cart

Use the [`POST /v1/shoppers/me/carts/active?expand=all`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request to apply an offer to a cart by including the applied product offers ([`appliedProductOffers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post)) object in the payload.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active?expand=all' \
--header 'Authorization: Basic {{access_token}}' \
...
--data-raw '{
  "cart": {
    "lineItems": {
      "lineItem": [
        {
          "quantity": 1,
          "product": {
            "id": 5181808200
          }
        }
      ],
      "appliedProductOffers": {
        "offer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        },
        "shippingOffer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        }
      }
    },
    "appliedOrderOffers": {
      "offer": {
        "offerId": "100029992",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      },
      "shippingOffer": {
        "offerId": "123111333",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      }
    }
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 OK` response.&#x20;

## Triggering an offer by cart

Use the [POST /v1/shoppers/me/carts/active](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post) request to trigger one or more product-level offers by cart.

{% hint style="info" %}
The offer type must be "Promotional URL / External Triggered Offer".
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: Basic {{access_token}}' \
...
--data-raw '{
  "lineItems": {
    "lineItem": [
      {
        "id": "488822300023",
        "quantity": 1,
        "product": {
          "id": "5181808200"
        }
      }
    ],
    "appliedProductOffers": {
      "offer": {
        "offerId": "882920011",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      },
      "shippingOffer": {
        "offerId": "882920011",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      }
    }
  }
}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items",
  "lineItems": [
    {
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
          "value": 101
        },
        "listPriceWithQuantity": {
          "currency": "USD",
          "value": 1010
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": 959.5
        },
        "formattedListPrice": "101.00USD",
        "formattedListPriceWithQuantity": "1010.00USD",
        "formattedSalePriceWithQuantity": "959.50USD",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": "240.00"
        },
        "productTax": {
          "currency": "USD",
          "value": "1.35"
        },
        "shippingTax": {
          "currency": "USD",
          "value": "0.65"
        },
        "feeTax": {
          "currency": "USD",
          "value": "2.00"
        },
        "taxRate": "0.1111",
        "importTax": {
          "currency": "USD",
          "value": 0
        },
        "formattedImportTax": "0.00USD",
        "importDuty": {
          "currency": "USD",
          "value": 0
        },
        "formattedImportDuty": "0.00USD"
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Trigging an offer by line items

Use the [`POST /line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/API-Trigger-Offer/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items%20\(API%20Trigger%20Offer\)/post) API to trigger one or more product-level offers at the line item.

{% hint style="info" %}
The offer type must be "Promotional URL / External Triggered Offer".
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items' \
--header 'Authorization: Basic {{access_token}}' \
...
--data-raw '{
  "cart": {
    "lineItems": {
      "lineItem": [
        {
          "quantity": 1,
          "product": {
            "id": "5181808200"
          }
        }
      ],
      "appliedProductOffers": {
        "offer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        },
        "shippingOffer": {
          "offerId": "882920011",
          "externalReferenceId": "unique-id",
          "customDescription": "Exclusive on our shop!!!"
        }
      }
    },
    "appliedOrderOffers": {
      "offer": {
        "offerId": "100029992",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      },
      "shippingOffer": {
        "offerId": "123111333",
        "externalReferenceId": "unique-id",
        "customDescription": "Exclusive on our shop!!!"
      }
    }
  }
}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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
    "lineItem": [
      {
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
            "value": 101
          },
          "listPriceWithQuantity": {
            "currency": "USD",
            "value": 1010
          },
          "salePriceWithQuantity": {
            "currency": "USD",
            "value": 959.5
          },
          "formattedListPrice": "101.00USD",
          "formattedListPriceWithQuantity": "1010.00USD",
          "formattedSalePriceWithQuantity": "959.50USD",
          "formattedCommitmentPrice": "$240.00",
          "commitmentPrice": {
            "currency": "USD",
            "value": "240.00"
          },
          "productTax": {
            "currency": "USD",
            "value": "1.35"
          },
          "shippingTax": {
            "currency": "USD",
            "value": "0.65"
          },
          "feeTax": {
            "currency": "USD",
            "value": "2.00"
          },
          "taxRate": "0.1111",
          "importTax": {
            "currency": "USD",
            "value": 0
          },
          "formattedImportTax": "0.00USD",
          "importDuty": {
            "currency": "USD",
            "value": 0
          },
          "formattedImportDuty": "0.00USD"
        }
      }
    ]
  },
  "totalItemsInCart": "1",
  "businessEntityCode": "DR_INC-ENTITY",
  "billingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
  },
  "shippingAddress": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
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
    "name": "Discover",
    "displayableNumber": "************4321",
    "expirationMonth": 0,
    "expirationYear": 2030
  },
  "paymentSession": {
    "id": "string",
    "status": "string",
    "clientSecret": "string",
    "redirectUrl": "https://api.digitalriver.com:80/payments/redirects/12759bb0-xxxx-4bdb-bfeb-9095ba8059fc?apiKey=a88fxxxx1eef47eb95bc609c22e593c8",
    "amountContributed": {
      "currency": "USD",
      "value": 1059.5
    },
    "amountRemainingToBeContributed": {
      "currency": "USD",
      "value": 1059.5
    }
  },
  "shippingOptions": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options"
  },
  "taxInclusive": true,
  "landedCostState": "NOT_ELIGIBLE",
  "pricing": {
    "subtotal": {
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
  "termsOfSalesAcceptance": "true",
  "chargeType": "moto",
  "customerType": "B",
  "taxRegistrations": [
    {
      "key": "UK_VAT",
      "value": "GB698588737"
    }
  ],
  "organizationId": "digitalriver12345"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

For more information see [API trigger offer source](../../../general-resources/shopper-apis-reference/carts/offers/api-trigger-offer.md#api-trigger-offer-source) and [API trigger offer query parameters](../../../general-resources/shopper-apis-reference/carts/offers/api-trigger-offer.md#api-trigger-offer-query-parameters).
