---
description: Learn how to retry a subscription update event.
---

# Retrying a subscription update event

If the subscription update event fails, Digital River will retry the subscription update event.

{% code title="Webhook request" overflow="wrap" %}
```json
{
   "type":"subscription.action.processed",
   "data":{
      "object":{
         "action":{
            "actionType":"ship_to_address",
            "actionStatus":"success"
         },
         "subscription":{
            "id":"13530199",
            "creationDate":"2022-06-01T09:14:48.000Z",
            "activationDate":"2022-06-01T05:00:00.000Z",
            "nextRenewalDate":"2022-07-01T05:00:00.000Z",
            "expirationDate":"2022-07-01T05:00:00.000Z",
            "graceDate":"2022-07-08T05:00:00.000Z",
            "currentQuantity":1,
            "renewalQuantity":1,
            "autoRenewal":true,
            "locale":"en_US",
            "state":"Subscribed",
            "duration":30,
            "frequency":30,
            "siteId":"sub2test",
            "shopper":{
               "id":"26195489030199"
            },
            "renewalPrice":{
               "unitPrice":10.99,
               "locked":false,
               "currency":"USD"
            },
            "term":{
               "termUnit":"MONTHS",
               "termLength":1
            },
            "product":{
               "id":"5363866300",
               "displayName":"Monthly auto renewal Subscription",
               "sku":"SUB_AUTORENEW"
            },
            "shipToAddress":{
               "id":"406032130199",
               "firstName":"Jane",
               "lastName":"Doe",
               "line1":"Abc",
               "city":"Pune",
               "postalCode":"324345",
               "countrySubdivision":"CA",
               "country":"AR",
               "countryName":"Argentina",
               "phoneNumber":"55534567890",
               "emailAddress":"subs_test@digitalriver.com"
            },
            "paymentOption":{
               "nickName":"Default",
               "id":"4022980199",
               "isDefault":"true",
               "type":"CreditCardMethod",
               "creditCard":{
                  "expirationMonth":"4",
                  "expirationYear":"2024",
                  "displayableNumber":"************1111",
                  "type":"visa",
                  "displayName":"Visa"
               },
               "address":{
                  "id":"406032100199",
                  "firstName":"Jane",
                  "lastName":"Doe",
                  "line1":"Abc",
                  "city":"Pune",
                  "postalCode":"324345",
                  "countrySubdivision":"CA",
                  "country":"AR",
                  "countryName":"Argentina",
                  "phoneNumber":"02134567890",
                  "emailAddress":"subs_test@digitalriver.com"
               }
            },
            "addOns":[
                
            ]
         }
      }
   },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"13530199"
   }
}
```
{% endcode %}
