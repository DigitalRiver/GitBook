---
description: Understand the subscription credit card expired event.
---

# Subscription credit card expired event

When the credit card is about to expire, Digital River creates a `subscription.credit_card_expired` event.

{% code title="Webhook request" overflow="wrap" %}
```json
{
   "type":"subscription.credit_card_expired",
   "data":{
      "object":{
         "id":"4200199",
         "creationDate":"2022-03-28T15:09:36.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-06-28T05:00:00.000Z",
         "expirationDate":"2022-06-28T05:00:00.000Z",
         "graceDate":"2022-07-05T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":true,
         "locale":"en_US",
         "state":"Subscribed",
         "duration":92,
         "frequency":92,
         "siteId":"earth1",
         "shopper":{
            "id":"25448428670199"
         },
         "renewalPrice":{
            "unitPrice":35.99,
            "locked":true,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":3
         },
         "product":{
            "id":"5619730199",
            "externalReferenceId":"",
            "displayName":"3 Month auto-renew Sub - Copy",
            "sku":"SUB_ADDONS"
         },
         "shipToAddress":{
            "id":"405320220199",
            "firstName":"Digital",
            "lastName":"River QA",
            "line1":"10380 Bren Rd W",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"5555559519",
            "emailAddress":"subs_test@digitalriver.com"
         },
         "paymentOption":{
            "nickName":"Visa 1111",
            "id":"4013880199",
            "isDefault":"false",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"4",
               "expirationYear":"2022",
               "displayableNumber":"************1111",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405320210199",
               "firstName":"Jane",
               "lastName":"Doe",
               "line1":"10380 Bren Rd W",
               "city":"Minnetonka",
               "postalCode":"55343",
               "countrySubdivision":"MN",
               "country":"US",
               "countryName":"United States",
               "phoneNumber":"5555559519",
               "emailAddress":"subs_test@digitalriver.com"
            }
         },
         "addOns":[
            {
               "product":{
                  "id":"5619750199",
                  "displayName":"Subscription AddOn_1 - Copy",
                  "sku":"SUB_ADDONS"
               },
               "quantity":1,
               "renewalPrice":{
                  "unitPrice":4.0,
                  "locked":true,
                  "currency":"USD"
               }
            }
         ]
      }
   },
   "clientIds":{
      "site_id":"earth1"
   },
   "searchableData":{
      "subscriptionId":"4200199"
   }
}
```
{% endcode %}
