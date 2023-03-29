---
description: Understand the subscription renewed event.
---

# Subscription renewed event

When a subscription is renewed, Digital River creates a `subscription.renewed` event and notifies your application when a successful subscription renewal event occurs.

At the end of a subscription period, the shopper must renew the subscription for continued access to the product. A shopper can accomplish a renewal in two ways:

* **Automatic Renewal (Auto Renew)**–The shopper provides a payment method that the system automatically debits a specified number of days before the subscription expiration date. If the renewal fails because the billing information is not correct (for example, an expired credit card) shoppers are notified and given a chance to update their billing information. Digital River will attempt to bill a shopper for automatic renewals several times. After which Digital River will cancel the subscription and list the billing attempt as failed.
* **Manual Renewal**–The shopper receives emails at preconfigured time intervals before the expiration date that asks the shopper to complete a renewal transaction. The shopper has to renew the subscription manually. The customer can choose one of the following options to renew their product:
  * Log in to their My Account portal and renew using the features available in the self-service options.
  * Call Customer Service to renew the subscription.

In either case, the system renews the subscription when the payment is complete.

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "subscription.renewed",
  "data": {
    "object": {
      "id": "8457000397",
      "creationDate": "2021-07-01T05:04:27.000Z",
      "activationDate": "2021-06-30T18:30:00.000Z",
      "nextRenewalDate": "2023-06-30T18:30:00.000Z",
      "expirationDate": "2023-06-30T18:30:00.000Z",
      "graceDate": "2023-07-30T18:30:00.000Z",
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
        "id": "5551000397",
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
