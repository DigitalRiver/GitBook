---
description: Learn how to retrieve a billing or shipping address from an order.
---

# Retrieving addresses from an order

## Retrieving the billing address from an order

To retrieve a billing address, use the [`GET /shoppers/me/orders/{orderId}/billing-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1billing-address/get) resource.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/billing-address' \
--header 'authorization: <a data-footnote-ref href="#user-content-fn-1">bearer </a>***\
...
</code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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

To retrieve a shipping address, use the [`GET /shoppers/me/orders/{orderId}/shipping-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1shipping-address/get) resource.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/shipping-address' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
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

[^1]: 
