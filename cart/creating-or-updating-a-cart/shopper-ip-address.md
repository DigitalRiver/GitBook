---
description: >-
  You can capture the IP address of the customer who placed the order.  Digital
  River uses this IP address to identify and prevent fraudulent activities.
---

# Capturing the customer's IP address

## Capturing the customer's IP format&#x20;

The Commerce API validates the format of the IP address and supports both IPv4 and IPv6 address schemes.

The following example uses IPv4:

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
POST /v1/shoppers/me/carts/active
```
{% endcode %}
{% endtab %}

{% tab title="Request body" %}
{% code overflow="wrap" %}
```json
{
   “cart”:{
      “ipAddress”:“192.16.1.1”
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example used IPv6:

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
POST /v1/shoppers/me/carts/active
```
{% endcode %}
{% endtab %}

{% tab title="Request body" %}
{% code overflow="wrap" %}
```json
{
   “cart”:{
      “ipAddress”:“2001:0000:3238:DFE1:63::FEFB”
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

If the call does not include an IP address, the call will work as originally designed. Digital River will not fail the order submission.

When a request captures an `ipAddress`, Digital River will use it to screen the order for fraud during submission.

When a connector (such as WordPress Plugin, Magento Extension, Salesforce B2B Commerce App, and so on) creates a cart, the connector collects all cart required data (including the customer's IP address, if available) before calling the [Cart ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper)resource. For these scenarios, the IP address should be sent in the Cart API call.

The following example uses IPv4:

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
POST /v1/shoppers/me/carts/active/submit-cart
```
{% endcode %}
{% endtab %}

{% tab title="Request body" %}
{% code overflow="wrap" %}
```json
{
 "cart": {
 "ipAddress":"192.179.12.1"
 }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example uses IPv6:

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
POST /v1/shoppers/me/carts/active/submit-cart
```
{% endcode %}
{% endtab %}

{% tab title="Request body" %}
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

## Validating the Customer's IP address

You can validate the customer's IP address was successfully captured by using the [`GET /shoppers/me`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/get) request. In the Response body, search for `ipAddress`. If the value of the `ipAddress` field is null, the client did not send an IP address for the customer. If the ipAddress is not null, run an IP search to verify the IP address, city, and state matches the customer address in the Global Commerce order. The IP address needs to be the customer's IP address and not the client server's IP address.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
GET /v1shoppers/me 
```
{% endcode %}
{% endtab %}

{% tab title="Request body" %}
{% code overflow="wrap" %}
```json
{
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
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Validation errors

If the IP address format is incorrect (that is, not in a valid IPv4 and IPv6 format), the API response will send a 409 Conflict error:

![409 Conflict error](<../../.gitbook/assets/409-conflict-error-invalid-ip-address (2) (1) (1).png>)
