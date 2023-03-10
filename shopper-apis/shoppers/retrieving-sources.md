---
description: Learn how to manage payment sources.
---

# Retrieving sources

For more information on payment options, see [Retrieving sources](../../payments/sources/retrieving-sources.md) under [Payments](broken-reference).

## Creating shopper payment options

Use the [`POST /v1/shoppers/me/payment-options`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) request to create payment options for a shopper.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/payment-options' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "paymentOption": {
    "nickName": "DRBank",
    "isDefault": "true",
    "sourceId": "c25fcccc-6e57-4d93-bafb-a6765510a422"
  },
  "shopper": {
    "ipAddress": "192.168.100.102"
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="201 Created response" %}
{% code overflow="wrap" %}
```json
{
  "paymentOptions": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options",
    "paymentOption": [
      {
        "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
        "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options/740865108",
        "id": 15699113789,
        "nickName": "Default",
        "isDefault": "true"
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Updating the shopper's payment options

Use the [`POST /v1/shoppers/me/payment-options/{paymentOptionId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options\~1%7BpaymentOptionId%7D/post) request with the payment options identifier (`paymentOptionId`) to update the shopper's payment options.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/payment-options/{paymentOptionid}' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "paymentOption": {
    "nickName": "DRBank",
    "isDefault": "true",
    "sourceId": "c25fcccc-6e57-4d93-bafb-a6765510a422"
  },
  "shopper": {
    "ipAddress": "192.168.100.102"
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options/740865108",
  "id": 740865108,
  "nickName": "Default",
  "isDefault": "true",
  "type": "creditCard",
  "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
  "sourceClientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
  "creditCard": {
    "expirationYear": "2030",
    "lastFourDigits": "0000",
    "clientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
    "expirationMonth": "08",
    "fundingSource": "debit",
    "brand": "Visa",
    "reusable": "true"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting the shopper's payment options

Use [`GET /v1/shoppers/me/payment-options`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options) request to retrieve all payment options configured for a shopper.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/payment-options' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "paymentOptions": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options",
    "paymentOption": [
      {
        "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
        "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options/740865108",
        "id": 15699113789,
        "nickName": "Default",
        "isDefault": "true"
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting the shopper's payment option

Use [`GET /v1/shoppers/me/payment-options/{paymentOptionId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options\~1%7BpaymentOptionId%7D/get) request with the payment options identifier (`paymentOptionId`) to retrieve all payment options configured for a shopper.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/payment-options/{paymentOptionId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "paymentOption": {
    "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
    "sourceClientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
    "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options/740865108",
    "id": 740865108,
    "nickName": "Default",
    "isDefault": "true",
    "type": "CreditCardMethod",
    "creditCard": {
      "expirationMonth": "1",
      "expirationYear": "2030",
      "brand": "Visa",
      "lastFourDigits": "1234"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
