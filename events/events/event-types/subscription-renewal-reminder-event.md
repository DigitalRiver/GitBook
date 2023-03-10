---
description: Understand the subscription renewal reminder event.
---

# Subscription renewal reminder event

When a subscription reaches the [renewal notification date](../../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/subscription-lifecycle.md), Digital River creates a `subscription.renewal_reminder` event. You can use this event to remind your customer to renew their subscription.

{% hint style="info" %}
When you create a webhook using this event, it combines the auto-renewal reminder, manual renewal reminder, and SEPA auto-renewal reminder into one event. As a result, we renamed the `subscription.auto_reminder` to `subscription.renewal_reminder`.
{% endhint %}

{% code title="Webhook request" overflow="wrap" %}
```json
{
   "type":"subscription.renewal_reminder",
   "data":{
      "object":{
         "id":"6310199",
         "creationDate":"2022-03-28T16:51:10.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-05-28T05:00:00.000Z",
         "nextBillingDate":"2022-05-28T05:00:00.000Z",
         "expirationDate":"2022-05-28T05:00:00.000Z",
         "graceDate":"2022-06-04T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":false,
         "locale":"en_US",
         "state":"Subscribed",
         "duration":61,
         "frequency":30,
         "currentBillingCycleNumber":2,
         "totalNumberOfBillingCycle":2,
         "siteId":"sub2test",
         "shopper":{
            "id":"25448437760199"
         },
         "renewalPrice":{
            "unitPrice":19.0,
            "locked":true,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":1
         },
         "product":{
            "id":"5403551500",
            "displayName":"APM_2_months_manual",
            "sku":"SUBS_COMMITMENT"
         },
         "shipToAddress":{
            "id":"405367800199",
            "firstName":"Jane",
            "lastName":"Doe",
            "line1":"10380 Bren Rd.",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"5555559519",
            "emailAddress":"subs_test@digitalriver.com"
         },
         "paymentOption":{
            "nickName":"Default",
            "id":"4018890199",
            "isDefault":"true",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"6",
               "expirationYear":"2026",
               "displayableNumber":"************1111",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405367320199",
               "firstName":"Digital",
               "lastName":"River QA",
               "line1":"10380 Bren Rd.",
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
             
         ]
      }
   },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"6310199"
   }
}
```
{% endcode %}
