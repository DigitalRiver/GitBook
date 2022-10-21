---
description: Learn how to get a subscription by using the subscription identifier.
---

# Getting a subscription by ID

The following [`GET /v1/subscriptions/{subscriptionId}`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getSubscriptionInfo) request changes the subscription renewal price. You need to provide the `subscriptionId` and the `renewalUnitPrice`. Note that the `renewalUnitPrice` cannot be higher than the existing price.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://{host}//v1/subscriptions/{subscriptionId}' \
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
    "id": "10499",
    "creationDate": "2020-10-05T11:59:53.000Z",
    "activationDate": "2020-10-05T05:00:00.000Z",
    "nextRenewalDate": "2021-10-05T05:00:00.000Z",
    "expirationDate": "2021-10-05T05:00:00.000Z",
    "graceDate": "2021-10-05T05:00:00.000Z",
    "currentQuantity": 1,
    "renewalQuantity": 1,
    "autoRenewal": false,
    "locale": "en_US",
    "state": "Subscribed",
    "duration": 365,
    "frequency": 365,
    "siteId": "sub2test",
    "term": {
        "termUnit": "YEARS",
        "termLength": 1
    },
    "product": {
        "id": "5396391800",
        "name": "Annual manual renewal Subscription"
    },
    "shipToAddress": {
        "id": "325333930516",
        "firstName": "John",
        "lastName": "Smith",
        "companyName": "Acme Company",
        "line1": "1234 Fake Street",
        "city": "Minnetonka",
        "postalCode": "55343",
        "countrySubdivision": "MN",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "5556543210",
        "emailAddress": "jsmith@acme.com"
    },
    "paymentOption": {
        "nickName": "Default",
        "id": "4010780499",
        "isDefault": "true",
        "type": "CreditCardMethod",
        "creditCard": {
            "expirationMonth": "2",
            "expirationYear": "2021",
            "displayableNumber": "************1111",
            "type": "visa",
            "displayName": "Visa"
        },
        "address": {
            "id": "325333930515",
            "firstName": "John",
            "lastName": "Smith",
            "companyName": "Acme Company",
            "line1": "1234 Fake Street",
            "city": "Minnetonka",
            "postalCode": "55343",
            "countrySubdivision": "MN",
            "country": "US",
            "countryName": "United States",
            "phoneNumber": "55343",
            "emailAddress": "jsmith@acme.com"
        }
    },
    "addOns": [ 
        {
          "product": {
            "id": "SubProd1234561",
            "name": "this is sub product addon1",
            "externalReferenceID": "32323377"
          },
          "quantity": 2
        },        
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
