---
description: Learn how to override a promotional URL offer discount.
---

# Overriding a promotional URL offer discount

This feature allows you to trigger the Promotional URL Offer type using a Commerce API and override the discount pass-in through an API from Global Commerce Merchandising offers when the Skip Offer Arbitration flag is enabled.

## High-level workflow use case

1. The user applies an offer ID or O-ERID to a cart to trigger Global Commerce's preconfigured offer behavior.
2. The client sets up a Promotional URL triggered offer in Global Commerce. A call to the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts)resource triggers the offer and applies the discount offer with the offer ID or ERID included in the call.
3. The system triggers this offer, then applies the new override discount to it. The term "Override or Overriden" specified here indicates the replacement of Global Commerce's Offer Discount setting.
4. The shopper can see the correct discount applied to the cart.
5. The shopper successfully submits the order.
6. The user triggers the Get Order resource (`GET /v1/shoppers/me/orders/[orderId]`).
7. The user can see the override description.

## The schema for skip offer arbitration via the Purchase resource

This schema applies to a [skip offer arbitration](skipping-global-commerce-merchandising-offer-arbitration.md).

{% tabs %}
{% tab title="Request samples" %}
{% code overflow="wrap" %}
```http
POST /shoppers/me/carts/active/line-items
POST /shoppers/me/carts/active/line-items/{id}
```
{% endcode %}
{% endtab %}

{% tab title="Payload sample" %}
{% code overflow="wrap" %}
```json
{
   "lineItems": {
      "lineItem": {
         "quantity": "1",
         "product": {
            "id": "4878374"
         }
      },
       "appliedProductOffers": {
          "offer": {
             "offerId": "23456",
             "customDescription": "Exclusive on our shop!!!",
             "overrideDiscount": [
                {
                   "externalReferenceId": "123",
                   "discount": 50,
                   "discountType": "amountOff"
                },
                {
                   "productId": "456",
                   "discount": 60,
                   "discountType": "amountOff"
                }
             ]
          },
          "shippingOffer": {
             "externalReferenceId": "23001",
             "customDescription": "Our prices are cheapest~~",
             "overrideDiscount": [
                {
                   "productId": "123",
                   "discount": 50,
                   "discountType": "amountOff"
                },
                {
                   "externalReferenceId": "456",
                   "discount": 60,
                   "discountType": "amountOff"
                }
             ]
          }
       }
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## The schema for a trigger offer or override discount via the Cart resource

This schema applies to a [trigger offer](triggering-a-promotional-url-offer.md) or an [override discount](overriding-a-promotional-url-offer-discount.md).

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```javascript
POST /shoppers/me/carts/active?skipOfferArbitration=true&offerId=12345&pid=1234
```
{% endcode %}
{% endtab %}

{% tab title="Payload sample" %}
{% code overflow="wrap" %}
```json
{
   "cart": {
      "lineItems": {
         "lineItem": [
            {
               "quantity": "1",
               "product": {
                  "id": "4878374"
               },
               "pricing": {
                  "salePrice": {
                     "currency": "USD",
                     "value": 8.99
                  }
               }
            }
         ],         
         "appliedProductOffers": {
            "offer": {
               "offerId": "23456",
               "customDescription": "Exclusive on our shop!!!",
               "overrideDiscount": [
                  {
                     "productId": "123",
                     "discount": 50,
                     "discountType": "amountOff"
                  },
                  {
                     "externalReferenceId": "456",
                     "discount": 60,
                     "discountType": "amountOff"
                  }
               ]
            },
            "shippingOffer": {
               "externalReferenceId": "23001",
               "customDescription": "Our prices are cheapest~~",
               "overrideDiscount": [
                  {
                     "productId": "123",
                     "discount": 50,
                     "discountType": "amountOff"
                  },
                  {
                     "externalReferenceId": "456",
                     "discount": 60,
                     "discountType": "amountOff"
                  }
               ]
            }
         }
      },
      "appliedOrderOffers": {
         "offer": {
            "offerId": "12345",
            "customDescription": "This is the finest offer you can get!!",
            "overrideDiscount": {
               "discount": 50,
               "discountType": "amountOff"
            }
         },
         "shippingOffer": {
            "externalReferenceId": "23000",
            "customDescription": "You earned a big money!",
            "overrideDiscount": {
               "discount": 10,
               "discountType": "percentOff"
            }
         }
      }      
   }
}

{
   "cart": {
      "lineItems": {
         "lineItem": [
            {
               "quantity": "1",
               "product": {
                  "id": "4878374"
               },
               "pricing": {
                  "salePrice": {
                     "currency": "USD",
                     "value": 8.99
                  }
               }
            }
         ],         
         "appliedProductOffers": {
            "offer": {
               "offerId": "23456",
               "customDescription": "Exclusive on our shop!!!",
               "overrideDiscount": [
                  {
                     "productId": "123",
                     "discount": 50,
                     "discountType": "amountOff"
                  },
                  {
                     "externalReferenceId": "456",
                     "discount": 60,
                     "discountType": "amountOff"
                  }
               ]
            },
            "shippingOffer": {
               "externalReferenceId": "23001",
               "customDescription": "Our prices are cheapest~~",
               "overrideDiscount": [
                  {
                     "productId": "123",
                     "discount": 50,
                     "discountType": "amountOff"
                  },
                  {
                     "externalReferenceId": "456",
                     "discount": 60,
                     "discountType": "amountOff"
                  }
               ]
            }
         }
      },
      "appliedOrderOffers": {
         "offer": {
            "offerId": "12345",
            "customDescription": "This is the finest offer you can get!!",
            "overrideDiscount": {
               "discount": 50,
               "discountType": "amountOff"
            }
         },
         "shippingOffer": {
            "externalReferenceId": "23000",
            "customDescription": "You earned a big money!",
            "overrideDiscount": {
               "discount": 10,
               "discountType": "percentOff"
            }
         }
      }      
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Terms

### Skip Offer Arbitration flag

Specify this flag in a query parameter at the cart level.

* **SkipOfferArbitration=TRUE**—Disables the Global Commerce Merchandising Offer arbitration logic to find the best price for a product.\
  \
  **Example**: Displays the Base Price.\
  \
  **Note**: If you pass the override discount offer on the same call, this offer will compete with other Global Commerce merchandising offers in the arbitration logic.
* **SkipOfferArbitration=FALSE**—Enables the Global Commerce Merchandising Offer arbitration logic to find the best price for a product.\
  \
  **Note**: If you pass the override discount offer on the same call, this offer will compete with other Global Commerce merchandising offers in the arbitration logic. The best offer wins.

### O-ERID

Offer-external reference ID. A unique external reference identifier for a specific offer. The client manages all associated business logic that defines when to apply the offer. You must specify this value at the site level to use it in Commerce API calls.

### Offer ID

Offer identifier. A unique Digital River identifier for a specific offer.

### Override or Overridden offer

When specified in this situation, it indicates there is a replacement for Global Commerce's Offer Discount setting. Don't confuse this term with Skip Offer Arbitration logic. When used, the system proceeds with offer arbitration after there is an override with the promotional URL type discount.

### Offer Description

Overrides the offer's description in the cart AFTER adding the applicable products into the current requisition.
