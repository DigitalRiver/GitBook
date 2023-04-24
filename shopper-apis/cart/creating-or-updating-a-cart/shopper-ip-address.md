---
description: >-
  You can capture the IP address of the customer who placed the order.  Digital
  River uses this IP address to identify and prevent fraudulent activities.
---

# Capturing the customer's IP address

## Capturing the customer's IP address

To capture a customer's IP address, provide the IP address in the payload of the [`POST /v1/shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request. The Commerce API validates the format of the IP address and supports both IPv4 and IPv6 address schemes.

If the call does not include an IP address, the call will work as originally designed. Digital River will not fail the order submission.

When a request captures an `ipAddress`, Digital River will use it to screen the order for fraud during submission.

### IPv4 example

The following [`POST /v1/shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request uses [IPv4](https://en.wikipedia.org/wiki/Internet\_Protocol\_version\_4).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: bearer {{access_token}}' \
...
--data-raw '{
   “cart”:{
      “ipAddress”: “192.16.1.1”
   }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 Successful` response.

### IPv6 example

The following [`POST /v1/shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request uses [IPv6](https://en.wikipedia.org/wiki/IPv6).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: bearer {{access_token}}' \
...
--data-raw '{
   “cart”:{
      “ipAddress”:“2001:0000:3238:DFE1:63::FEFB”
   }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 Successful` response.

## Collecting the IP address through a connector

When a connector (such as WordPress Plugin, Magento Extension, Salesforce B2B Commerce App, and so on) creates a cart, the connector collects all cart required data (including the customer's IP address, if available) before calling the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource. For these scenarios, the IP address should be sent in the [`POST /v1/shoppers/me/carts/active/submit-cart`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) request.

### IPv4 example

The following [`POST /v1/shoppers/me/carts/active/submit-cart`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) request uses [IPv4](https://en.wikipedia.org/wiki/Internet\_Protocol\_version\_4).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http

curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active/submit-cart' \
--header 'Authorization: bearer {{access_token}}' \
...
--data-raw '{
 "cart": {
 "ipAddress":"192.179.12.1"
 }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 Successful` response.

### IPv6 example

The following the [`POST /v1/shoppers/me/carts/active/submit-cart`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) request uses [IPv6](https://en.wikipedia.org/wiki/IPv6).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active/submit-cart' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: applicati0n/json'
...
--data-raw '{
 "cart": {
 "ipAddress":"2001:0000:3238:DFE1:63::FEFB"
 }
}'
```
{% endcode %}
{% endtab %}

{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
 "cart": {
 "ipAddress":"2001:0000:3238:DFE1:63::FEFB"
 }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 Successful` response.

## Validating the Customer's IP address

You can validate the successful capture of a customer's IP address by using the [`GET v1/shoppers/me`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/get) request. In the response body, search for `ipAddress`. If the value of the `ipAddress` field is null, you did not send the customer's IP address. If the `ipAddress` is not null, run an IP search to verify the IP address, city, and state matches the customer address in the Global Commerce order. The IP address must be the customer's IP address and not your server's IP address.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request GET' https://api.digitalriver.com/v1/shoppers/me ' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: applicati0n/json'
...
--data-raw '{
    "shopper": {
        "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me",
        "id": 495796950789,
        "username": "myu_external",
        "externalReferenceId": "myu_external@digitalriver.com",
        "firstName": "Marc",
        "lastName": "Yu",
        "emailAddress": "myu_external@digitalriver.com",
        "locale": "en_US",
        "currency": "USD",
        "sendMail": "false",
        "sendEmail": "false",
        "ipAddress": "192.179.12.1",
        "paymentOptions": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options",
            "paymentOption": [
                {
                    "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/payment-options/13821416689",
                    "id": 13821416689,
                    "nickName": "default",
                    "isDefault": "false",
                    "type": "CreditCardMethod",
                    "creditCard": {
                        "expirationMonth": 12,
                        "expirationYear": 2022,
                        "issueCode": null,
                        "startMonth": null,
                        "startYear": null,
                        "displayableNumber": "************1111",
                        "type": "visa",
                        "displayName": "Visa"
                    }
                }
            ]
        },
        "addresses": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/addresses"
        },
        "orders": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/orders"
        },
        "subscriptions": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/subscriptions"
        }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `200 Successful` response.

## Validation errors

If the IP address format is incorrect (that is, not in a valid IPv4 and IPv6 format), the API response will send a `409 Conflict` error:

![409 Conflict error](<../../../.gitbook/assets/409-conflict-error-invalid-ip-address (2).png>)
