---
description: Learn how to lookup orders.
---

# Order lookup

The [Order Lookup](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Order-Lookup) resource lets you retrieve information about an order.

## Get your current order

You can retrieve your current order. This method requires an authenticated customer token, username, and password.

This call can retrieve information such as the customer's email address, the last 4 digits of their payment card, and their password.

{% tabs %}
{% tab title="URI" %}
```http
POST shoppers/order-lookup
```
{% endtab %}

{% tab title="Request header" %}
```http
Host: api.digitalriver.com
Accept: application/json
Authorization: bearer your_access_token
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_102)
```
{% endtab %}

{% tab title="Request body" %}
```javascript
orderId=your_order_ID&&username=userName&password=orderPassword
```
{% endtab %}

{% tab title="Response header" %}
```javascript
HTTP/1.1 200 OK
```
{% endtab %}

{% tab title="Response body" %}
```javascript
{
  "orders": {
    "order": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/100009222210019",
        "id": 100009222210019,
        "submissionDate": "2018-05-04T17:12:17.000Z",
        "pricing": {
          "total": {
            "currency": "USD",
            "value": "19.99"
          },
          "formattedTotal": "$13.95"
        },
        "payment": {
          "paymentMethodName": "discover",
          "displayableNumber": "************9876"
        },
        "orderState": "Complete",
        "billingAddress": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
          "id": "billingAddress",
          "firstName": "Automation",
          "lastName": "Tester",
          "line1": "PO BOX 6930",
          "line2": "123",
          "line3": "Suite Line 3",
          "city": "Waconia",
          "countrySubdivision": "MN",
          "postalCode": 5387,
          "country": "US",
          "countryName": "United States",
          "phoneNumber": "099-222-44454",
          "emailAddress": "automatedTester68091904@digitalriver.com"
        },
        "shippingAddress": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/address/47278020023",
          "id": "billingAddress",
          "firstName": "Automation",
          "lastName": "Tester",
          "line1": "PO BOX 6930",
          "line2": "123",
          "line3": "Suite Line 3",
          "city": "Waconia",
          "countrySubdivision": "MN",
          "postalCode": 5387,
          "country": "US",
          "countryName": "United States",
          "phoneNumber": "099-222-44454",
          "emailAddress": "automatedTester68091904@digitalriver.com"
        }
      }
    ],
    "totalResults": 1,
    "totalResultPages": 1
  }
}
```
{% endtab %}
{% endtabs %}

## Retrieve the current order by email address and the last 4 digits of their payment card

Use the [`POST /shoppers/order-lookup`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Order-Lookup/paths/\~1v1\~1shoppers\~1order-lookup/post) to retrieve a customer's current order. An authenticated customer token, email address, and last 4 digits of their payment card are required.

{% tabs %}
{% tab title="URI" %}
```http
POST shoppers/order-lookup?expand=all
```
{% endtab %}

{% tab title="Request header" %}
```http
Host: api.digitalriver.com
Accept: application/x-www-form-urlencoded
Authorization: bearer your_access_token
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_102)
```
{% endtab %}

{% tab title="Request body" %}
```javascript
creditCardLastDigits=last_4_digits_of_their_payment_card&emailAddress=shopper's_email_address
```
{% endtab %}

{% tab title="Response header" %}
```http
HTTP/1.1 200 OK
```
{% endtab %}

{% tab title="Response body" %}
```javascript
{"orders": {
   "order": [   {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999",
      "id": 9999999999,
      "submissionDate": "2016-11-02T14:25:06.000Z",
      "locale": "en_US",
      "testOrder": "false",
      "pricing":       {
         "total":          {
            "currency": "USD",
            "value": 13.88
         },
         "formattedTotal": "$13.88"
      },
      "payment":       {
         "paymentMethodName": "discover",
         "displayableNumber": "************9876"
      },
      "orderState": "Complete",
      "billingAddress":       {
         "id": "billingAddress",
         "firstName": "John",
         "lastName": "Doe",
         "line1": "PO BOX 3940",
         "city": "Waconia",
         "countrySubdivision": "MN",
         "postalCode": "55387",
         "phoneNumber": "555-555-555",
         "emailAddress": "jdoe@gmail.com"
      },
      "shippingAddress":       {
         "id": "billingAddress",
         "firstName": "John",
         "lastName": "Doe",
         "line1": "PO BOX 3940",
         "city": "Waconia",
         "countrySubdivision": "MN",
         "postalCode": "55387",
         "phoneNumber": "555-555-555",
         "emailAddress": "jdoe@gmail.com"
      }
   }],
   "totalResults": 1,
   "totalResultPages": 1
}}
```
{% endtab %}
{% endtabs %}

##
