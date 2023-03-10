---
description: Learn how to create a customer.
---

# Creating a customer

This topic describes how to create a customer account record. Creating a customer account is necessary for an anonymous customer that does not yet have an account created for a site, and a site does not provide a guest checkout. In this instance, the site requires a customer to have an account to purchase a product. Creating a customer is not necessary for an anonymous customer who is only browsing products.

You can make this request without an access token by passing in your API key as a query parameter. You can also send this request with either a valid anonymous or authenticated customer token.

Send a [POST shoppers](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers/post) request with the customer's information in the request payload.

The following example shows a request with an access token:

{% tabs %}
{% tab title="cURL with an access token" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example shows passes in your API key instead of an access token:

{% tabs %}
{% tab title="cURL  without an access token" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers?apiKey=your_api_key' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

The content required for the payload depends on who maintains the master record for the customer's username and password information. The base customer account information includes the customer's name and email address. The following list displays the minimum resource fields required for the Shoppers resource to create a customer record:

* `username`
* `password` (base64 encoded)
* `emailAddress`
* `externalReferenceId`
* `firstName`
* `lastName`

If Digital River maintains the master record for the customer login credentials, the payload must contain the `username` and `password`. The customer's `password` must be base64 encoded.

{% hint style="info" %}
**Best Practices**: Explicitly set the `locale` and `currency` for a customer at the start of a session.
{% endhint %}

{% tabs %}
{% tab title="Payload sample for Digital River-maintained master record" %}
{% code overflow="wrap" %}
```json
{
   "shopper": {
      "username": "myShopper@myCompany.com",
      "password": "cFGzc3dvcmQ=",
      "firstName": "John",
      "lastName": "Johnson",
      "emailAddress": "jjohnson@myCompany.com",
      "locale": "en_US",
      "currency": "USD"
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

If your company maintains the master record for the customer login credentials, the payload must contain the `externalReferenceId`.

{% tabs %}
{% tab title="Payload sample for the client-maintained master record" %}
{% code overflow="wrap" %}
```json
{
   "shopper": {
      "username": "myShopper@myCompany.com",
      "password": "cFGzc3dvcmQ=",
      "firstName": "John",
      "lastName": "Johnson",
      "emailAddress": "jjohnson@myCompany.com",
      "locale": "en_US",
      "currency": "USD"
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The response returned from the server is an HTTP Status 201 Created.

Now that the base customer record has been created, you can get an authenticated customer token and send the [`GET shoppers/me/account`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Account/paths/\~1v1\~1shoppers\~1me\~1account/get) request to allow the customer to log in and configure his or her account information. The account information associated with a customer includes the shipping address, billing address, and payment options.
