---
description: Learn how to use a single-click checkout.
---

# Single-click checkout

Use a single-click checkout to purchase a product on behalf of a customer during an authenticated customer session. This resource bypasses calling the [Apply Shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper) and [Submit Cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart) resources separately and instantly purchases a single product. A typical example of a product purchased via this API is an auto-renewal, such as a subscription.

The product-direct purchase API performs the following actions with one Shopper API call:

1. Adds a product to the cart.
2. Applies the default customer address to the cart.
3. Applies the default payment option to the cart.
4. Submits the cart.
5. Creates an order.

## Prerequisite

The request requires a valid authenticated customer token.

## Sending a product purchase request

Send a [Product ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1products\~1{productId}/get)request with the specific product ID for the product that the customer wants to purchase.&#x20;

{% tabs %}
{% tab title="cURL" %}
The following request sample purchases a product with a product ID of 291233200.

{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/products/291233200/purchase' \
--header 'Authorization: bearer {{access_token}}' \ 
...
```
{% endcode %}
{% endtab %}

{% tab title="201 Created response" %}
The response header contains a `Location` header, as shown on line `4`, to the order created for the transaction. The order identifier is `1234567890`. The request and response bodies are empty.

{% code overflow="wrap" lineNumbers="true" %}
```http
HTTP/1.1 201 Created
Server: Apache
X-Server-Name: server.xyz.digitalriverws.net
Location: https://api.digitalriver.com/shoppers/me/orders/1234567890
Content-Length: 0
Accept-Ranges: bytes
Date: Fri, 17 Jan 2014 16:46:30 GMT
Age: 0
Access-Control-Allow-Origin: *
HTTP/1.1 201 Created
Server: Apache
X-Server-Name: server.xyz.digitalriverws.net
Location: https://api.digitalriver.com/shoppers/me/orders/1234567890
Content-Length: 0
Accept-Ranges: bytes
Date: Fri, 17 Jan 2014 16:46:30 GMT
Age: 0
Access-Control-Allow-Origin: *
```
{% endcode %}
{% endtab %}
{% endtabs %}

No further calls are required. If applicable, you can make follow-up calls to get the order by its identifier or the order history for the customer.
