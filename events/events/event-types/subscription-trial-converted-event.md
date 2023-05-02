---
description: Understand the trial converted event.
---

# Subscription trial converted event

When a trial has been automatically or manually converted to a paid subscription, Digital River creates the `subscription.trial_converted` event

{% code title="Webhook request" overflow="wrap" %}
```json
{
    "type": "subscription.trial_converted",
    "data": {
        "object": {
            "id": "15548700289",
            "creationDate": "2022-03-29T06:58:53.000Z",
            "activationDate": "2022-03-29T05:00:00.000Z",
            "nextRenewalDate": "2023-07-02T05:00:00.000Z",
            "expirationDate": "2023-07-02T05:00:00.000Z",
            "graceDate": "2023-07-09T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": true,
            "locale": "en_US",
            "state": "Subscribed",
            "duration": 365,
            "frequency": 365,
            "siteId": "sub2test",
            "shopper": {
                "id": "504462170289",
                "externalReferenceId": "PBFYTT3GAYPV"
            },
            "renewalPrice": {
                "unitPrice": 15.0,
                "locked": false,
                "currency": "USD"
            },
            "term": {
                "termUnit": "YEARS",
                "termLength": 1
            },
            "product": {
                "id": "5523771400",
                "displayName": "Trial Auto Product - DO NOT EDIT OR MODIFY",
                "sku": "TRIRENREM"
            },
            "shipToAddress": {
                "id": "330009650289",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "Digital River",
                "line1": "10380 Bren Rd W",
                "line2": "Conjunto 304",
                "line3": "Conjunto 304",
                "city": "Minnetonka",
                "postalCode": "55343",
                "countrySubdivision": "MN",
                "country": "US",
                "countryName": "United States",
                "phoneNumber": "555-253-1234",
                "emailAddress": "subs_test@digitalriver.com",
                "countyName": "Minnetonka"
            },
            "paymentOption": {
                "nickName": "VisaEIB9RB",
                "id": "16063790289",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "3",
                    "expirationYear": "2024",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "330113400289",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "Digital River",
                    "line1": "10380 Bren Rd W",
                    "line2": "Conjunto 304",
                    "line3": "Conjunto 304",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "countrySubdivision": "MN",
                    "country": "US",
                    "countryName": "United States",
                    "phoneNumber": "555-253-1234",
                    "emailAddress": "subs_test@digitalriver.com",
                    "countyName": "Minnetonka"
                }
            },
            "addOns": []
        }
    },
    "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"15548700289"
   }
}
```
{% endcode %}
