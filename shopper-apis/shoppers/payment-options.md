---
description: Learn how to manage payment options.
---

# Payment options

## Creating shopper payment options

Use the [`POST /v1/shoppers/me/payment-options`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) request to create payment options for a shopper. See [Payment options query parameters](../../general-resources/shopper-apis-reference/shoppers/payment-options.md) for a description of the query parameters.&#x20;

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

{% tab title="201 Created" %}
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

&#x20;See [Retrieving sources](retrieving-sources.md) and [Payment options](../../general-resources/shopper-apis-reference/shoppers/payment-options.md) for more information.
