---
description: Learn how to lookup orders.
---

# Order lookup

The [Order Lookup](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Order-Lookup) resource lets you retrieve information about an order.

## Retrieve the order by order ID and order password

You can [retrieve your order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Order-Lookup/paths/\~1v1\~1shoppers\~1order-lookup/post). This request requires the [anonymous shopper token](../oauth/tokens.md#creating-an-anonymous-shopper-session-guest-checkout), an order identifier (`orderId`), and an order password (`password`).

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http"><strong>curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/order-lookup?expand=all' \
</strong>--header 'authorization: Basic ***\
--header 'Accept: application/json' \
--header 'Content-Type: application/x-www-form-urlencoded' \
...
--data-urlencode 'orderId=order_id' \
--data-urlencode 'password=order_password'

</code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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
{% endcode %}
{% endtab %}
{% endtabs %}

See the [Order lookup query parameters](../../general-resources/shopper-apis-reference/orders.md#order-lookup-query-parameters) for more information.

## Retrieve the order by email address and the last four digits of their payment card

You can [retrieve a customer's current order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Order-Lookup/paths/\~1v1\~1shoppers\~1order-lookup/post). This request requires the customer's [authenticated shopper token](../oauth/tokens.md#initiating-an-authenticated-session-returning-shopper-or-login-shopper), email address, and the last four digits of their payment card.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/order-lookup?expand=all' \
--header 'authorization: Basic ***\
--header 'Accept: application/json' \
--header 'Content-Type: application/x-www-form-urlencoded' \
...
--data-urlencode 'creditCardLastDigits=last_4_digits_of_their_payment_card' \
--data-urlencode 'emailAddress=shopper's_email_address'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
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
{% endcode %}
{% endtab %}
{% endtabs %}

See the [Order lookup query parameters](../../general-resources/shopper-apis-reference/orders.md#order-lookup-query-parameters) for more information.
