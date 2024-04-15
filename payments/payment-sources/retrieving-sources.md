---
description: >-
  Learn how to retrieve a single Source as well as all the Source objects
  attached to a Customer.
---

# Retrieving sources

## Get a Source object by identifier

The following [`GET/sources/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources) request retrieves a source by supplying its unique identifier as a path parameter.

{% hint style="info" %}
This identifier was returned when you used the [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started) library to [create the source](../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-sources).
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request GET 'https://api.digitalriver.com/sources/e59c8303-139a-4077-bd26-78d20b43d52b' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '<API_key>' \
```
{% endtab %}
{% endtabs %}

The response returns a [Source object](./) if a valid identifier and API key are provided in the request. The following sample response shows a [credit card type](./#determining-the-payment-method-type) Source in a [chargeable state](./#source-state).

{% hint style="warning" %}
Only the last four digits of credit card numbers are returned by a `GET` Source request.
{% endhint %}

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "e59c8303-139a-4077-bd26-78d20b43d52b",
    "createdTime": "2020-06-17T19:54:54Z",
    "type": "creditCard",
    "currency": "USD",
    "amount": 24.89,
    "reusable": true,
    "state": "chargeable",
    "customerId": "517796760336",
    "owner": {
        "firstName": "William",
        "lastName": "Brown",
        "email": "apiTester@digitalriver.com",
        "address": {
            "line1": "10380 Bren Road West",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        }
    },
    "paymentSessionId": "8ff5840f-b0ec-44f2-8e88-647627a0ba0d",
    "clientSecret": "e59c8303-139a-4077-bd26-78d20b43d52b_5e943931-e4e7-4537-8ae4-f7ff991f463c",
    "creditCard": {
        "brand": "MasterCard",
        "expirationMonth": 5,
        "expirationYear": 2025,
        "lastFourDigits": "0008"
    },
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

## Obtain a customer's sources

You can retrieve the [Sources](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources) associated with a Customer by making a [get Customer by identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCustomers) request and then parsing the `sources` array contained in the response.

The following `GET/customers/{id}` request supplies the identifier as a path parameter:

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request GET 'https://api.digitalriver.com/customers/517796760336' \
--header 'Authorization: Bearer <API_key>' \
```
{% endtab %}
{% endtabs %}

In the response, each element of the `sources` array consists of a [Source object](./) attached to the Customer. In this particular response, the array contains two elements, which means the customer has two saved payment methods, both [reusable](./#reusable-or-single-use) and [chargeable](./#source-state).

{% tabs %}
{% tab title="JSON" %}
```javascript
...
"sources": [
    {
        "id": "239f7e2a-1efe-45fd-af81-76eeb9aa3eb9",
        "createdTime": "2020-06-02T18:24:49Z",
        "type": "creditCard",
        "currency": "USD",
        "amount": 57.69,
        "reusable": true,
        "state": "chargeable",
        "owner": {
            "firstName": "William",
            "lastName": "Brown",
            "email": "apiTester@digitalriver.com",
            "address": {
                "line1": "10380 Bren Road West",
                "city": "Minnetonka",
                "postalCode": "55343",
                "state": "MN",
                "country": "US"
            }
        },
        "paymentSessionId": "07ed3298-8ed8-4e22-a298-d53c110663b3",
        "clientSecret": "239f7e2a-1efe-45fd-af81-76eeb9aa3eb9_ac8c566e-2155-4919-befb-06f78a43480f",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 7,
            "expirationYear": 2027,
            "lastFourDigits": "1111"
        }
    },
    {
        "id": "e59c8303-139a-4077-bd26-78d20b43d52b",
        "createdTime": "2020-06-17T19:54:54Z",
        "type": "creditCard",
        "currency": "USD",
        "amount": 24.89,
        "reusable": true,
        "state": "chargeable",
        "owner": {
            "firstName": "William",
            "lastName": "Brown",
            "email": "apiTester@digitalriver.com",
            "address": {
                "line1": "10380 Bren Road West",
                "city": "Minnetonka",
                "postalCode": "55343",
                "state": "MN",
                "country": "US"
            }
        },
        "paymentSessionId": "8ff5840f-b0ec-44f2-8e88-647627a0ba0d",
        "clientSecret": "e59c8303-139a-4077-bd26-78d20b43d52b_5e943931-e4e7-4537-8ae4-f7ff991f463c",
        "creditCard": {
            "brand": "MasterCard",
            "expirationMonth": 5,
            "expirationYear": 2025,
            "lastFourDigits": "0008"
        }
    }
],
...
```
{% endtab %}
{% endtabs %}

### Display a customer's sources

The data contained in the `sources` array can display a customer's saved payment methods on your website or app. To do this, parse the response and extract the values in the `creditCard`, `owner`, and `address` hash tables. You can then use these values to present the card's brand name, last four digits, expiration date, and the customer's billing information.
