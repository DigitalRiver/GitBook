---
description: Learn how to retrieve a billing or shipping address from an order.
---

# Retrieving addresses from an order

## Retrieving the billing address from an order

To retrieve a billing address, use the `G`[`ET /shoppers/me/orders/{orderId}/billing-address`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1billing-address/get) resource.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
GET shoppers/me/orders/9999999999/billing-address
```
{% endcode %}
{% endtab %}

{% tab title="Request header" %}
{% code overflow="wrap" %}
```http
Host: api.digitalriver.com
Accept: application/json
Authorization: bearer your_access_token
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_102)
```
{% endcode %}
{% endtab %}

{% tab title="Payload" %}
{% code overflow="wrap" %}
```
The request body should be empty. 
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```javascript
{"address": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/billing-address",
   "id": "billingAddress",
   "firstName": "John",
   "lastName": "Doe",
   "companyName": "null",
   "line1": "PO BOX 3940",
   "line2": "123",
   "line3": null,
   "city": "Waconia",
   "countrySubdivision": "MN",
   "postalCode": "55387",
   "country": "US",
   "countryName": "United States",
   "phoneNumber": "555-555-555"
}}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Retrieving the shipping address from an order

To retrieve a shipping address, use the [`GET /shoppers/me/orders/{orderId}/shipping-address`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1shipping-address/get) resource.

{% tabs %}
{% tab title="URI" %}
```http
GET shoppers/me/orders/9999999999/shipping-address
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

{% tab title="Payload" %}
```
The request body should be empty. 
```
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```javascript
{"address": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/shippingAddress",
   "id": "shippingAddress",
   "firstName": "John",
   "lastName": "Doe",
   "companyName": "null",
   "line1": "PO BOX 3940",
   "line2": "123",
   "line3": null,
   "city": "Waconia",
   "countrySubdivision": "MN",
   "postalCode": "55387",
   "country": "US",
   "countryName": "United States",
   "phoneNumber": "555-555-5555"
}}
```
{% endcode %}
{% endtab %}
{% endtabs %}
