---
description: Learn how to get a shopper's subscription.
---

# Getting a shopper's subscription

The following [`GET /v1/subscriptions?shopperId={shopperId}`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getSubscriptionsInfo) request gets a shopper's subscription using the shopper's identifier or ERID. You need to provide the shopper identifier (`shopperId`) or external reference identifier (`ERID`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://{host}//v1/subscription?shopperId={shopperId or ERID}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "subscriptions": [
    {
      "id": "14554435010",
      "externalReferenceId": "subext123232",
      "creationDate": "2020-06-12T06:49:21.000Z",
      "activationDate": "2020-06-12T00:00:00.000Z",
      "nextRenewalDate": "2020-07-02T05:00:00.000Z",
      "expirationDate": "2020-07-12T05:00:00.000Z",
      "graceDate": "2020-07-12T00:00:00.000Z",
      "cancellationDate": null,
      "currentQuantity": 4,
      "renewalQuantity": 2,
      "autoRenewal": true,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 30,
      "frequency": 30,
      "currentBillingCycleNumber": 0,
      "totalNumberOfBillingCycle": 0,
      "siteId": "sub2test",
      "term": {
        "termUnit": "MONTHS",
        "termLength": "1"
      },
      "product": {
        "id": "SubProd1234561",
        "name": "This is sub product",
        "externalReferenceID": "32323323"
      },
      "shipToAddress": {
        "id": "123232213",
        "firstName": "Jane", 
        "lastName": "Doe", 
        "companyName": "Acme Company", 
        "line1": "1234 Fake Street",
        "line2": "Apt. 2", 
        "city": "Minnetonka",
        "countrySubdivision": "MN",
        "postalCode": "55343",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-253-1234",
        "emailAddress": "jdoe@acme.com"
      },
      "paymentOption": {
        "id": "14827725210",
        "nickName": "Visa 1111",
        "isDefault": "false",
        "type": "CreditCardMethod",
        "sourceId": "323223232323",
        "creditCard": {
          "expirationMonth": "11",
          "expirationYear": "2034",
          "displayableNumber": "fadfafafdfadafad",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "123232213",
          "firstName": "Jane", 
          "lastName": "Doe", 
          "companyName": "Acme Company", 
          "line1": "1234 Fake Street",
          "line2": "Apt. 2", 
          "city": "Minnetonka",
          "countrySubdivision": "MN",
          "postalCode": "55343",
          "country": "US",
          "countryName": "United States",
          "phoneNumber": "555-253-1234",
          "emailAddress": "jdoe@acme.com"
        }
      },
      "addOns": [
        {
          "product": {
            "id": "SubProd1234561",
            "name": "This is sub-product addon1",
            "externalReferenceID": "32323377"
          },
          "quantity": 2
        },
        {
          "product": {
            "id": "B123",
            "name": "This is another sub product",
            "externalReferenceID": "32323555"
          },
          "quantity": 1
        }
      ]
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
