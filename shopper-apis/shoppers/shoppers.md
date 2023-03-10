---
description: Learn how to manage shoppers.
---

# Shoppers

## Creating a current shopper

Use [`POST /v1/shoppers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers/post) to create a shopper record. Contact your Digital River team to set up this request.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "shopper": {
    "username": "jswanson@digitalriver.com",
    "firstName": "Jason",
    "lastName": "swanson",
    "emailAddress": "jswanson@digitalriver.com",
    "password": "qwerasdf",
    "locale": "en_US",
    "currency": "USD",
    "sendMail": true,
    "sendEMail": true
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="201 Created response" %}
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

## Updating a current shopper

Use [`POST /v1/shoppers/me`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post) to update the current shopper's data. The information you can update depends on the type of access token you are currently using. If you have an anonymous shopper token and are therefore updating an anonymous shopper, you can only update the IP address, locale, and currency. Updating shopper information beyond that requires an authenticated shopper token. You can update all shopper information including username and password for an authenticated shopper.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "shopper": {
    "username": "jswanson@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jswanson@digitalriver.com",
    "password": "qwerasdf",
    "locale": "en_US",
    "currency": "USD",
    "sendMail": true,
    "sendEMail": true
  }
}'
```
{% endcode %}
{% endtab %}

{% tab title="204 Successful response" %}
{% code overflow="wrap" %}
```json
{
  "shopper": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me",
    "id": 1234567890,
    "username": "jswanson@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jswanson@digitalriver.com",
    "paymentOptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options"
    },
    "addresses": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
    },
    "orders": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
    },
    "subscriptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting a current shopper

Use [`GET /v1/shoppers/me`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers) to get the current shopper's data for both anonymous and authenticated shoppers.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "shopper": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me",
    "id": 1234567890,
    "username": "jswanson@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jswanson@digitalriver.com",
    "paymentOptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options"
    },
    "addresses": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
    },
    "orders": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
    },
    "subscriptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
