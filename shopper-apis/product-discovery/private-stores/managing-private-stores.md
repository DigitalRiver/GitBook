---
description: Lear how to manage private stores.
---

# Managing private stores

## Getting a private store

Use the [`GET /v1/shoppers/me/purchase-plan`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan/paths/\~1v1\~1shoppers\~1me\~1purchase-plan/get) to retrieve the details for a private store.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/purchase-plan' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "id": "11859200",
  "isAuthenticationRequiredToBrowse": "false",
  "purchasePlanName": "Copy of @EmailDomain",
  "brandDisplayName": "@EmailDomain",
  "targetMarketId": "35600",
  "targetMarketName": "@EmailDomain"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Purchase private store parameters](../../../general-resources/shopper-apis-reference/private-store.md#private-store-query-parameters) for more information.

## Searching for a private store

Use [`GET /v1/shoppers/me/purchase-plan/search`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Search/paths/\~1v1\~1shoppers\~1me\~1purchase-plan\~1search/get) and provide the relevant query parameters to search for a private store.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/purchase-plan/search' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/purchase-plan/search",
  "purchasePlan": [
    {
      "currency": "USD",
      "value": "19.99"
    }
  ],
  "totalResults": "2"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Search private store query parameters](../../../general-resources/shopper-apis-reference/private-store.md#search-private-store-query-parameters) for more information.

## Authorizing a purchase plan

Use [POST /v1/shoppers/me/purchase-plan/-authorize](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Authorize/paths/\~1v1\~1shoppers\~1me\~1purchase-plan\~1authorize/post) to authenticate the current shopper session for a specific private store. Note that some private stores may have more than one configured access rule.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/purchase-plan/authorize' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="204 No Content" %}
You will receive a `204 No Content` response.
{% endtab %}
{% endtabs %}

See [Authorize private store query parameters](../../../general-resources/shopper-apis-reference/private-store.md#authorize-private-store-query-parameters) for more information,
