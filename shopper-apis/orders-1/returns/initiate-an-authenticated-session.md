---
description: Learn how to initiate an authenticated session for a return.
---

# Initiate an authenticated session

Use the `GET /oauth20/authorize` to send the following request to [create an authenticated shopper token](../../../resources/API-structure/#creating-authenticated-shopper-tokens) to identify the shopper session:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/oauth20/token.json' \
--header 'authorization: Basic ***\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

Include your base64-encoded API key and secret in the request header. Include `grant_type=client_credentials` and the `externalReferenceId` in the request body. This Token API identifies a shopper session. A token consists of the `access_token` and the `refresh_token`. They correspond to the session cookie and the cookie in the browser. You can save the `access_token` and `refresh_token` in the application and use them in subsequent queries. The `access_token` expires after a specified interval (60 minutes by default in user session site settings in Global Commerce). The `refresh_token` expires after one year.

The `expires_in` property is the time-to-live (TTL) value for the access token. You can refresh the access token at any time.
