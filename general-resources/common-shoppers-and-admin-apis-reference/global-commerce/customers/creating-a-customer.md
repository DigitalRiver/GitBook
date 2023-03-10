---
description: Learn how to create a customer.
---

# Creating a customer

You can make this request without an access token by passing in your API key as a query parameter. You can also send this request with either an anonymous customer or an authenticated customer token.

## POST requests

Send a `POST /shoppers` request to the [Shopper ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers)resource with the customer's information in the request payload.

To send a request with an access token:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

To send a request without an access token, include your API key:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me?apiKey=your_api_key' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Shopper object

The content required for the payload depends on who maintains the master record for the customer's username and password information. The base customer account information includes the customer's name and email address.&#x20;

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" %}
```json
{
  "shopper": {
    "username": "jswanson@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jswanson@digitalriver.com",
    "password": "qwerasdf",
    "locale": "en_US",
    "currency": "USD",
    "sendMail": true,
    "sendEMail": true
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following list displays the minimum [Shopper ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers)resource fields required to create a customer record:

* `username`
* `password` (base64 encoded)
* `emailAddress`
* `externalReferenceId`
* `firstName`
* `lastName`
* `locale`– Required for landed costs.
* `currency`– Required for landed costs
