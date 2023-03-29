---
description: Understand the subscription created event.
---

# Subscription created event

When a customer purchase a new subscription, Digital River creates a `subscription.created` event.

During the shopping experience, a customer orders a subscription to one of your products. They may order a trial subscription or a purchased subscription.

If you [created a webhook](../../webhooks/creating-a-webhook.md) using the `subscription.created` event for your application (endpoint URL), Digital River notifies your application when a successful subscription acquisition event occurs.

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "subscription.created",
  "data": {
    "object": {
      "id": "8457000397",
      "creationDate": "2021-07-01T05:04:47.493Z",
      "activationDate": "2021-06-30T18:30:00.000Z",
      "nextRenewalDate": "2022-06-30T18:30:00.000Z",
      "expirationDate": "2022-06-30T18:30:00.000Z",
      "graceDate": "2022-07-30T18:30:00.000Z",
      "currentQuantity": 1,
      "renewalQuantity": 1,
      "autoRenewal": true,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 365,
      "frequency": 365,
      "siteId": "sub2test",
      "shopper": {
        "id": "35504010397"
      },
      "renewalPrice": {
        "unitPrice": 95,
        "locked": false,
        "currency": "USD"
      },
      "term": {
        "termUnit": "YEARS",
        "termLength": 1
      },
      "product": {
        "id": "9964801100",
        "displayName": "Annual Auto Renewal Subscription",
        "sku": "12"
      },
      "shipToAddress": {
        "id": "76213030397",
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "ABC",
        "line1": "Kalyani Nagar",
        "city": "Pune",
        "postalCode": "411014",
        "countrySubdivision": "AA",
        "country": "IN",
        "countryName": "India",
        "phoneNumber": "55503796942",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "paymentOption": {
        "nickName": "Default",
        "id": "6631000397",
        "isDefault": "true",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "8",
          "expirationYear": "2023",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "66287380397",
          "firstName": "Jane",
          "lastName": "Doe",
          "companyName": "ABC",
          "line1": "Kalyani Nagar",
          "city": "Pune",
          "postalCode": "411014",
          "countrySubdivision": "AA",
          "country": "IN",
          "countryName": "India",
          "phoneNumber": "55503796942",
          "emailAddress": "subs_test@digitalriver.com"
        }
      },
      "addOns": []
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "8457000397"
  }
}
```
{% endcode %}
