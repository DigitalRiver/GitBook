---
description: Understand the subscription payment failed event.
---

# Subscription payment failed event

When the subscription payment attempt fails, Digital River creates a `subscription.payment_failed` event. You will receive a notification that includes the reason why the customer's transaction failed. Note that this event is only applicable to auto-renewal.

{% hint style="info" %}
PayPal and other payment methods share the same events. However, the contents of the email notification for each payment method will be different.
{% endhint %}

We include the payment method in the webhook payload for each notification.

{% code title="Webhook request" overflow="wrap" %}
```json
{
   "type":"subscription.payment_failed",
   "data":{
      "object":{
         "id":"5610199",
         "creationDate":"2022-03-28T16:29:13.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-05-28T05:00:00.000Z",
         "nextBillingDate":"2022-05-28T05:00:00.000Z",
         "expirationDate":"2022-05-28T05:00:00.000Z",
         "graceDate":"2022-06-04T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":true,
         "locale":"en_US",
         "state":"PendingRenewal",
         "duration":61,
         "frequency":30,
         "currentBillingCycleNumber":2,
         "totalNumberOfBillingCycle":2,
         "siteId":"sub2test",
         "shopper":{
            "id":"25448436960199",
            "externalReferenceId":"OXELSH53JI9L"
         },
         "renewalPrice":{
            "unitPrice":9.0,
            "locked":false,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":1
         },
         "product":{
            "id":"5367865200",
            "displayName":"APM_2_months_auto",
            "sku":"SUBS_COMMITMENT"
         },
         "shipToAddress":{
            "id":"405361290199",
            "firstName":"Jane",
            "lastName":"Doe",
            "companyName":"DR",
            "line1":"10380 Bren Rd W",
            "line2":"Conjunto 304",
            "line3":"Conjunto 304",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"555-253-1234",
            "emailAddress":"subs_test@digitalriver.com",
            "countyName":"Minnetonka"
         },
         "paymentOption":{
            "nickName":"VisaYVX7B2",
            "id":"4017490199",
            "isDefault":"true",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"3",
               "expirationYear":"2024",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405360070199",
               "firstName":"Jane",
               "lastName":"Doe",
               "companyName":"DR",
               "line1":"10380 Bren Rd W",
               "line2":"Conjunto 304",
               "line3":"Conjunto 304",
               "city":"Minnetonka",
               "postalCode":"55343",
               "countrySubdivision":"MN",
               "country":"US",
               "countryName":"United States",
               "phoneNumber":"555-253-1234",
               "emailAddress":"subs_test@digitalriver.com",
               "countyName":"Minnetonka"
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
      "subscriptionId":"5610199"
   }
}
```
{% endcode %}
