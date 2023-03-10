---
description: >-
  Learn how to retrieve a single source as well as all the Source objects
  attached to a customer.
---

# Retrieving sources

## Get a source object by identifier

The following [`GET/sources/{id}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/retrieveSources) request retrieves a source by supplying its unique identifier as a path parameter.

{% hint style="info" %}
This identifier was returned when you used the [DigitalRiver.js](../payments-solutions/digitalriver.js/) library to [create the source](../../general-resources/reference/digitalriver-object.md#creating-sources).
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/sources/e59c8303-139a-4077-bd26-78d20b43d52b' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '<API_key>' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

If a valid identifier and API key are provided, the response returns a [source object](./). This sample response returns a [credit card source type](./#source-types) in a [`chargeable` state](./#source-state).

{% hint style="warning" %}
Only the last four digits of credit card numbers are returned by a `GET /source` request.
{% endhint %}

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
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
{% endcode %}
{% endtab %}
{% endtabs %}

### Display a customer's sources

The data contained in the `sources` array can be used to display a customer's saved payment methods on your website or app. To do this, parse the response and extract the values in the `creditCard`, `owner`, and `address` hash tables. You can then use these values to present the card's brand name, last four digits, expiration date, and the customer's billing information.

## Obtain a shopper's sources

You can retrieve the [sources ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)associated with a shopper's payment option by making a [get current shopper](../../shopper-apis/shoppers/shoppers.md#getting-a-current-shopper) request and parsing the `paymentOptions` object contained in the response if the payment source is attached to the shopper's payment option. One payment option can contain one payment source. When the shopper gets their payment options, all payment sources will be listed.

### Step 1: Create your first payment source and option

1. Create your first payment source using either [DigitalRiver.js](../payments-solutions/digitalriver.js/) or [Drop-in Payments](../payments-solutions/drop-in/).
2. Create your first payment option using: \
   [`POST /v1/shoppers/me/payment-options/`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post)``

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/payment-options/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
  "paymentOption" : {
    "nickName" : "Credit Card",
    "isDefault" : "true",
    "sourceId":"{{sourceId1}}"
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 2: Create your second payment source and option

1. Create your second payment source using either [DigitalRiver.js](../payments-solutions/digitalriver.js/) or [Drop-in Payments](../payments-solutions/drop-in/).
2. Create your second payment option using: \
   [`POST /v1/shoppers/me/payment-options/`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post)``

{% tabs %}
{% tab title="Request body" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/payment-options/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
  "paymentOption" : {
    "nickName" : "PayPal",
    "isDefault" : "true",
    "sourceId":"{{sourceId2}}"
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 3: Get the shopper's payment options

Get the shopper's payment options using: [`GET /v1/shoppers/me/payment-options/`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/get).

{% tabs %}
{% tab title="Response body" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/payment-options/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "paymentOptions": {
        "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options",
        "paymentOption": [
            {
                "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options/15578475589",
                "nickName": "Credit Card",
                "isDefault": "false",
                "sourceId": "7e49fddb-9b64-453c-bd22-1231b4cb1819"
            },
            {
                "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options/15578475689",
                "nickName": "PayPal",
                "isDefault": "true",
                "sourceId": "7e49fddb-9b64-453c-bd22-1231b4cb2316"
            }
        ]
    }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}
