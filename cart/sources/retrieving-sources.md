---
description: >-
  Learn how to retrieve a single Source as well as all the Source objects
  attached to a Customer.
---

# Retrieving sources

## Get a Source object by identifier

The following request [retrieves a Source](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources). You only need to supply the unique source identifier [returned by DigitalRiver.js](../../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in) and your secret API key.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request GET 'https://api.digitalriver.com/sources/e59c8303-139a-4077-bd26-78d20b43d52b' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '<API_key>' \
```
{% endtab %}
{% endtabs %}

If a valid identifier and API key are provided, the response returns a Source object. This sample response returns a Source with a `type` of `creditCard` and a state of `chargeable`.&#x20;

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

## Obtain a shopper's sources

You can retrieve the [Sources](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources) associated with a Shopper by making a [get Customer by ID](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCustomers) request and parsing the `sources` array contained in the response if the payment source is attached to the shopper's payment option.  When the shopper gets their payment options, all payment sources will be listed.

### Step 1: Create your first payment source and option

1. Create your first payment source using: \
   `POST https://{{dispatchHost}}/payments/sources/`
2. Create your first payment option using: \
   `POST http://{{dispatchHost}}/v1/shoppers/me/payment-options/`

{% tabs %}
{% tab title="cURL" %}
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
{% endtab %}
{% endtabs %}

### Step 2: Create your second payment source and option

1. Create your second payment source using: \
   `POST https://{{dispatchHost}}/payments/sources/`
2. Create your second payment option using: \
   `POST https://{{dispatchHost}}/v1/shoppers/me/payment-options/`

{% tabs %}
{% tab title="Request body" %}
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
{% endtab %}
{% endtabs %}

### Step 3: Get the shopper's payment options

Get the shopper's payment options using: `GET https//{{dispatchHost}}/v1/shoppers/me/payment-options/`

{% tabs %}
{% tab title="Response body" %}
```javascript
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
                "isDefault": "false"
            },
            {
                "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options/15578475689",
                "nickName": "PayPal",
                "isDefault": "true"
            }
        ]
    }
}'
```
{% endtab %}
{% endtabs %}

### Display a customer's sources

The data contained in the `sources` array can be used to display a customer's saved payment methods on your website or app. To do this, parse the response and extract the values in the `creditCard`, `owner`, and `address` hash tables. You can then use these values to present the card's brand name, last four digits, expiration date, and the customer's billing information.
