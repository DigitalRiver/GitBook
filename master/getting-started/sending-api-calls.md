---
description: Learn how to send API calls using either /auth or an API key.
---

# Sending API calls

## API calls that require an API key and shopper token

When accessing [Shopper APIs](broken-reference) such as the [shoppers](../../shopper-apis/shoppers/), [account](../../shopper-apis/shoppers/account.md), [addresses](../../shopper-apis/shoppers/addresses.md), [product discovery](../../shopper-apis/product-discovery/), [cart](../../shopper-apis/cart/), [orders](../../shopper-apis/orders-1/), and [subscriptions](broken-reference), you need a [confidential API key](../../resources/API-structure/api-keys.md#confidential-keys) with [Shopper APIs permission](roles-and-permissions.md#commerce-api-suite-roles-and-permissions) and a shopper token.&#x20;

## API calls that only require an API key

When accessing [Admin APIs](broken-reference) for [product management](../../admin-apis/product-management/), and [subscriptions management](../../admin-apis/subscription-management/), use a [confidential API key](../../resources/API-structure/api-keys.md#confidential-keys) with [Admin APIs permission](roles-and-permissions.md#commerce-api-suite-roles-and-permissions).

## API calls that require an API key and `/auth`

For [refund management](../../admin-apis/returns-and-refunds-1/), use a [confidential API key](../../resources/API-structure/api-keys.md#confidential-keys) with [Admin APIs permission](roles-and-permissions.md#commerce-api-suite-roles-and-permissions) and `/auth`.&#x20;

## Sending an API call using `/auth`

If you want to send a [Refunds ](../../admin-apis/returns-and-refunds-1/)request, you must supply your [confidential API key](../../resources/API-structure/api-keys.md#confidential-keys) with `/auth`. Include your Global Commerce username and encoded password with the `/auth`. Global Commerce will authenticate the credentials.

{% hint style="success" %}
**Hint**: When using a Postman collection,  provide your Global Commerce credentials in the  `csrUserName` and `csrPassword` fields.
{% endhint %}

For example, a Global Commerce user with the Customer Service Director, Customer Service Supervisor, or Customer Service Representative role can access the `/auth` service to get the `access_token` and then use that `access_token` to [create a satisfaction refund](../../admin-apis/returns-and-refunds-1/creating-a-satisfaction-refund.md).

{% tabs %}
{% tab title="POST /auth" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https:///api.digitalriver.com/auth' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Accept: application/json' \
--header 'Authorization: Basic {{confidential_key}}=' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username={{username}}' \
--data-urlencode 'password={{password}}'
```
{% endcode %}
{% endtab %}
{% endtabs %}
