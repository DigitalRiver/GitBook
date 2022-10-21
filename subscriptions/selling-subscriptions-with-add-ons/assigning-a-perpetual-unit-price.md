---
description: Learn how to assign a perpetual unit price to a subscription with add-ons.
---

# Assigning a perpetual unit price

## Assigning a perpetual unit price to a subscription

In this scenario, you assign a perpetual unit price to a customer's subscription.

Use the [`POST /v1/subscriptions/{subscriptionId}/perpetual-price`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/changePerpetualPrice) resource to assign a perpetual unit price to a customer's subscription. You need to include the subscription identifier (`subscriptionId`) and the perpetual unit price (`perpetUnitPrice`). In the following example, the value for the product's `perpetualUnitPrice` is `120` and the value for the add-on's `perpetualUnitPrice` is `50`.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/perpetual-price' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
    "perpetualUnitPrice": 120,
    "addOns": [
        {
            "product": {
                "externalReferenceId": "A123"
            },
            "perpetualUnitPrice": 20
        },
        {
            "product": {
                "id": "B456"
            },
            "perpetualUnitPrice": 50
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

## Creating a cart with a perpetual unit price

In this scenario, you create a cart and assign a perpetual unit price to a customer's subscription.

Use the [`POST /v1/shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) or the [`POST /v1/shoppers/me/carts/active/line-items`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post) resource to create a cart request. You need to include the perpetual unit price (`perpetualUnitPrice`) in the subscription override info (`subscriptionOverrideInfo`).&#x20;

{% tabs %}
{% tab title="/active cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/shoppers/me/carts/active' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
    "cart": {
        "lineItems": {
            "lineItem": [
                {
                    "quantity": "1",
                    "product": {
                        "id": "5363866300"
                    },
                    "customAttributes": {
                        "attribute": [
                            {
                                "name": "groupIdForAddon",
                                "value": "9814462289"
                            }
                        ]
                    },
                    "subscriptionOverrideInfo": {
                        "perpetualUnitPrice": {
                            "currencyCode": "USD",
                            "amount": 49.99
                        }
                    }
                },
                {
                    "quantity": "1",
                    "product": {
                        "id": "5400082600"
                    },
                    "customAttributes": {
                        "attribute": [
                            {
                                "name": "groupIdForAddon",
                                "value": "9814462289"
                            },
                            {
                                "name": "parentProductIdForAddon",
                                "value": "5363866300"
                            }
                        ]
                    },
                    "subscriptionOverrideInfo": {
                        "perpetualUnitPrice": {
                            "currencyCode": "USD",
                            "amount": 39.99
                        }
                    }
                }
            ]
        }
    }
}'
```
{% endtab %}

{% tab title="/line-items cURL" %}
```javascript
curl --location --request POST 'https://<<host>>/v1/shoppers/me/carts/line-items' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
    "cart": {
        "lineItems": {
            "lineItem": [
                {
                    "quantity": "1",
                    "product": {
                        "id": "5363866300"
                    },
                    "customAttributes": {
                        "attribute": [
                            {
                                "name": "groupIdForAddon",
                                "value": "9814462289"
                            }
                        ]
                    },
                    "subscriptionOverrideInfo": {
                        "perpetualUnitPrice": {
                            "currencyCode": "USD",
                            "amount": 49.99
                        }
                    }
                },
                {
                    "quantity": "1",
                    "product": {
                        "id": "5400082600"
                    },
                    "customAttributes": {
                        "attribute": [
                            {
                                "name": "groupIdForAddon",
                                "value": "9814462289"
                            },
                            {
                                "name": "parentProductIdForAddon",
                                "value": "5363866300"
                            }
                        ]
                    },
                    "subscriptionOverrideInfo": {
                        "perpetualUnitPrice": {
                            "currencyCode": "USD",
                            "amount": 39.99
                        }
                    }
                }
            ]
        }
    }
}'
```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response. The response to this request creates a shopping cart and returns an access token to be included in all other cart interactions.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "cart" : {
    "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active",
    "paymentMethods" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/payment-methods"
    },
    "webCheckout" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/web-checkout"
    },
    "id" : 861184190082,
    "lineItems" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/line-items",
      "lineItem" : [ {
        "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/line-items/10288020082",
        "id" : 10288020082,
        "quantity" : 1,
        "product" : {
          "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/products/5363866300",
          "displayName" : "Monthly auto renewal Subscription",
          "thumbnailImage" : null
        },
        "pricing" : {
          "listPrice" : {
            "currency" : "USD",
            "value" : 11.11
          },
          "listPriceWithQuantity" : {
            "currency" : "USD",
            "value" : 11.11
          },
          "salePriceWithQuantity" : {
            "currency" : "USD",
            "value" : 11.11
          },
          "formattedListPrice" : "$11.11",
          "formattedListPriceWithQuantity" : "$11.11",
          "formattedSalePriceWithQuantity" : "$11.11",
          "productTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "shippingTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "feeTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "taxRate" : 0,
          "importTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "formattedImportTax" : "$0.00",
          "importDuty" : {
            "currency" : "USD",
            "value" : 0
          },
          "formattedImportDuty" : "$0.00"
        }
      }, {
        "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/line-items/10288030082",
        "id" : 10288030082,
        "quantity" : 1,
        "product" : {
          "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/products/5400082600",
          "displayName" : "Subscription AddOn 1",
          "thumbnailImage" : null
        },
        "pricing" : {
          "listPrice" : {
            "currency" : "USD",
            "value" : 11
          },
          "listPriceWithQuantity" : {
            "currency" : "USD",
            "value" : 11
          },
          "salePriceWithQuantity" : {
            "currency" : "USD",
            "value" : 11
          },
          "formattedListPrice" : "$11.00",
          "formattedListPriceWithQuantity" : "$11.00",
          "formattedSalePriceWithQuantity" : "$11.00",
          "productTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "shippingTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "feeTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "taxRate" : 0,
          "importTax" : {
            "currency" : "USD",
            "value" : 0
          },
          "formattedImportTax" : "$0.00",
          "importDuty" : {
            "currency" : "USD",
            "value" : 0
          },
          "formattedImportDuty" : "$0.00"
        }
      } ]
    },
    "totalItemsInCart" : 2,
    "businessEntityCode" : "DR_INC-ENTITY",
    "billingAddress" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/billing-address"
    },
    "shippingAddress" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/shipping-address"
    },
    "payment" : { },
    "paymentSession" : {
      "id" : "2912a240-a65b-4ef5-bd2c-427b342b4dba",
      "clientSecret" : "2912a240-a65b-4ef5-bd2c-427b342b4dba_978f2dd6-eaef-4933-a460-5f6b917d2b35",
      "status" : "requires_source"
    },
    "shippingMethod" : { },
    "shippingOptions" : {
      "uri" : "https://dispatch-test.digitalriver.com/shop/sites/sub2test/shoppers/me/carts/active/shipping-options"
    },
    "taxInclusive" : "false",
    "landedCostState" : "NOT_ELIGIBLE",
    "pricing" : {
      "subtotal" : {
        "currency" : "USD",
        "value" : 22.11
      },
      "discount" : {
        "currency" : "USD",
        "value" : 0
      },
      "shippingAndHandling" : {
        "currency" : "USD",
        "value" : 0
      },
      "importTaxAndDuty" : {
        "currency" : "USD",
        "value" : 0
      },
      "tax" : {
        "currency" : "USD",
        "value" : 0
      },
      "orderTotal" : {
        "currency" : "USD",
        "value" : 22.11
      },
      "formattedSubtotal" : "$22.11",
      "formattedDiscount" : "$0.00",
      "formattedShippingAndHandling" : "$0.00",
      "formattedImportTaxAndDuty" : "$0.00",
      "formattedTax" : "$0.00",
      "formattedOrderTotal" : "$22.11"
    },
    "termsOfSalesAcceptance" : null
  }
}
```
{% endtab %}
{% endtabs %}

Apply the shopper and submit the cart using the  [Shoppers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers/post)resource.

## Creating or changing a perpetual unit price

In this scenario, you create or change a perpetual unit price to a customer's subscription.

Use the [`POST /v1/subscriptions/{subscriptionId}/perpetual-price`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/changePerpetualPrice) resource to apply a forever price for the remaining subscription cycle. You can use it to change a non-perpetual subscription to a perpetual subscription if the supplied subscription is not a perpetual subscription. You need to provide the `subscriptionId` and the `renewalUnitPrice`. Note that the `renewalUnitPrice` cannot be higher than the existing price.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl -X POST \
  https://{host}/v1/subscriptions/{subscription_Id}/perpetual-price \
  -H 'authorization: Basic ****' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 5cb141b9-8077-8b12-3eff-ebb45db3ffa6' \
  -d '{
        "perpetualUnitPrice" : 59.99
      }'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
