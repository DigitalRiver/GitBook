---
description: Learn how to get a shopper's account information.
---

# Account

## Getting the shopper account information

The [`GET /v1/shoppers/me/account`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Account/paths/\~1v1\~1shoppers\~1me\~1account/get) request allows shoppers to configure their account information. The request responds with a `302 Found` response with a redirect to a web page that allows a shopper to enter their billing address, shipping address, and payment information. This method requires an authenticated shopper token. See [Account query parameters](../../general-resources/shopper-apis-reference/shoppers/account.md#account-query-parameters) for a description of the query parameters.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/account' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response.
