---
description: Learn how to manage access tokens.
---

# Access tokens

## Getting an access token

Use the [`GET /oauth20/access-token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Access-Tokens/paths/\~1oauth20\~1access-tokens/get) to get an access token.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request GET 
'https://api.digitalriver.com/oauth20/access-token' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "sessionId": "your_session_ID",
  "userId": "your_user_ID",
  "externalReferenceId": "external_reference_ID",
  "authenticated": "true",
  "locale": "en_US",
  "currency": "USD",
  "cartId": "your_cart_ID",
  "clientIpAddress": "string",
  "domain": "drh-api-ot04.digitalriverws.net",
  "expiresIn": 86397,
  "themeId": "string",
  "sessionTag": "session_tag"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Deleting an access token

Use the [`DELETE /oauth20/access-token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Access-Tokens/paths/\~1oauth20\~1access-tokens/delete) to delete an access token.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request DELETE 'https://api.digitalriver.com/oauth20/access-token' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "sessionId": "your_session_ID",
  "userId": "your_user_ID",
  "externalReferenceId": "external_reference_ID",
  "authenticated": "true",
  "locale": "en_US",
  "currency": "USD",
  "cartId": "your_cart_ID",
  "clientIpAddress": "string",
  "domain": "drh-api-ot04.digitalriverws.net",
  "expiresIn": 86397,
  "themeId": "string",
  "sessionTag": "session_tag"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
