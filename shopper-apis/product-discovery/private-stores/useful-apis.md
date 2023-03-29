---
description: Learn about the most useful APIs when managing a Private Store.
---

# Useful APIs

## Getting an access token by session token

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/token.json?apiKey={{client_id}}&session_token={{session_token}}' \
--header 'authorization: bearer {{apikey_secret_authr}}\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Verifying the access token is authenticated

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/oauth20/access-tokens.json?token={{access_token}}' \
--header 'authorization: bearer {{apikey_secret_authr}}\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Searching for a private store

When you search for a Private Store, the `id` for `purchasePlanAuthorize` and the `targetMarketId` appears in the response. When you search for a Private Store, you need to provide `id` for the `purchasePlanAuthorize` and the `targetMarketId` in the request. Unless you frequently create and edit private stores, this step is not required. You should store or cache these attributes on your side.

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
    "purchasePlanAuthorize":{
        "id":"4912758700",
        "targetMarketId":"4897371800",
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

