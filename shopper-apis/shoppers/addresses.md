---
description: Learn how to manage addresses.
---

# Addresses

## Creating or updating a shopper's address

Use [`POST /v1/shoppers/me/addresses`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Addresses/paths/\~1v1\~1shoppers\~1me\~1addresses/post) to create a shopper record. Contact your Digital River team to set up this request. An address entry must have a unique nickname. If a current address has the same nickname specified in the request, that address is updated; otherwise, a new address is created.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http"><strong>curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/addresses' \
</strong>--header 'authorization: bearer ***\
...
--data-raw '{
  "address": {
    "nickName": "test",
    "isDefault": "true",
    "firstName": "Jon",
    "lastName": "Doe",
    "companyName": "Digital River",
    "line1": "10380 Bren Road West",
    "line2": "string",
    "line3": "string",
    "city": "Minnetonka",
    "countrySubdivision": "MN",
    "postalCode": "55343",
    "country": "US",
    "countryName": "United States",
    "countyName": "Hennepin",
    "phoneNumber": "555-253-1234",
    "phoneticFirstName": "クリス",
    "phoneticLastName": "ミラー",
    "division": "製品開発"
  }
}
</code></pre>
{% endtab %}
{% endtabs %}

You will receive a `204 No Content` response.

## Getting an address by identifier

Use [`GET /v1/shoppers/me/addresses/{addressId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Addresses/paths/\~1v1\~1shoppers\~1me\~1addresses\~1%7BaddressId%7D/get) to get an address by its identifier (`addressId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/addresses/{addressId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "address": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses/1234567890",
    "id": 1655007697,
    "nickName": "test",
    "isDefault": "true",
    "firstName": "Jon",
    "lastName": "Doe",
    "line1": "10380 Bren Road West",
    "line2": "string",
    "city": "Minnetonka",
    "countrySubdivision": "MN",
    "postalCode": "55343",
    "country": "US",
    "countryName": "United States",
    "phoneNumber": "952-253-1234",
    "phoneticFirstName": "クリス",
    "phoneticLastName": "ミラー",
    "division": "製品開発"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting all shopper addresses

Use [`GET /v1/shoppers/me/addresses`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Addresses/paths/\~1v1\~1shoppers\~1me\~1addresses/get) to get an address by its identifier (`addressId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/addresses' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "addresses": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses",
    "address": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses/1234567890",
        "nickName": "test",
        "isDefault": "true"
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Deleting a shopper's address

Use [DELETE /v1/shoppers/me/addresses/{addressId}](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Addresses/paths/\~1v1\~1shoppers\~1me\~1addresses\~1%7BaddressId%7D/delete) to delete a shopper's address.

{% tabs %}
{% tab title="cUR." %}
{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/v1/shoppers/addresses/{addressId}' \
--header 'authorization: bearer ***\
...De
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `204 No Content` response.
