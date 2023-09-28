---
description: Learn how to create a customer.
---

# Creating a customer

This topic describes how to create a customer account record. Creating a customer account is necessary for an anonymous customer when a site does not provide a guest checkout. In this instance, the site requires a customer to have an account before purchasing a product. Creating a customer is unnecessary for an anonymous customer only browsing products.

You can make this request without an access token by passing in your API key as a query parameter. You can also send this request with a valid anonymous or authenticated customer token.

## Creating a shopper

Send a [POST /v1/shoppers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers/post) request with the customer's information in the request payload. The request requires an access token or an API key.&#x20;

If Digital River maintains the master record for the customer login credentials, the request body must contain the `username` and `password`. The customer's `password` must be base64 encoded. If your company maintains the master record for the customer login credentials, the payload must contain the `externalReferenceId`.

{% hint style="info" %}
**Best Practices**: Explicitly set the `locale` and `currency` for a customer at the start of a session.
{% endhint %}

{% tabs %}
{% tab title="cURL for a Digital River-hosted shopper" %}
{% code overflow="wrap" %}
```javascript
curl --location 'https://api.digitalriver.com/v1/shoppers' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic {{access_token}}' \
--header 'Cookie: {{token}}' \
--data-raw '{
  "shopper": {
    "username": "jdoe@dr.com",
    "firstName": "Jane",
    "lastName": "Doe",
    "emailAddress": jdoe@dr.com,
    "password": "jdoepassword",
    "currency": "USD"    
    "locale": "en_US",
  }
}'
```
{% endcode %}
{% endtab %}

{% tab title="cURL for a client-hosted shopper" %}
{% code overflow="wrap" %}
```javascript
curl --location 'dispatch-api.digitalriver.com/v1/shoppers' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic {{access_token}}' \
--header 'Cookie: {{token}}' \
--data-raw '{
  "shopper": {
    "username": "jdoe@acme.com",
    "firstName": "Jane",
    "lastName": "Doe",
    "emailAddress": jdoe@acme.com,
    "currency": "USD"    
    "locale": "en_US",
    "externalReferenceId": "efe44307-ef82-46ed-bef4-e87ebec2ba28"
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

The required payload contents depend on who maintains the master record for the customer's username and password information. The base customer account information includes the customer's name and email address. The following list displays the minimum resource fields required for the Shoppers resource to create a customer record:

* `username`
* `password` (base64 encoded): Only required for a Digital River-hosted shopper. It is not required for a client-hosted shopper.
* `emailAddress`
* `externalReferenceId`: Only required for a client-hosted shopper.
* `firstName`
* `lastName`

The response returned from the server is an HTTP Status 201 Created.

You can get an authenticated customer token now that the base customer record has been created.

{% tabs %}
{% tab title="cURL with an access token" %}
{% code overflow="wrap" %}
```html
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers' \
--header 'Authorization: bearer {{access_token}}' \ 
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example passes in your API key instead of an access token:

{% tabs %}
{% tab title="Request sample without an access token" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers? apiKey=your_api_key' \ 
...
```
{% endcode %}
{% endtab %}
{% endtabs %}



