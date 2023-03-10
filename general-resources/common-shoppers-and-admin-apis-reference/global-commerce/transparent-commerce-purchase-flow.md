---
description: Understand the Transparent Commerce purchase flow.
---

# Transparent Commerce purchase flow

Use Transparent Commerce™ to instantly purchase a product on behalf of a customer during an authenticated customer session. This API bypasses calling the [Apply Shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper) and [Submit Cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart) resources separately and instantly purchases a single product. A typical example of a product purchased via this resource is auto-renewal, such as a subscription.

The product direct purchase API performs the following actions with one Shopper call:

1. Adds a product to the cart.
2. Applies the default customer address to the cart.
3. Applies the default payment option to the cart.
4. Submits the cart.
5. Creates an order.

{% hint style="info" %}
**Prerequisite**: The request must be made with a valid full access token.
{% endhint %}

Send the `POST shoppers/me/products/{productId}/purchase` request with the specific product ID for the product that the customer wants to purchase.&#x20;

The following example purchases a product with a product ID of `291233200`. The response header contains a `Location` header, as shown in line 4, to the order that was created for the transaction. The ID of the order is `1234567890`. The request and response bodies are empty.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/products/291233200/purchase' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="Response header" %}
{% code overflow="wrap" %}
```
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

No further calls are required. If applicable, you can make follow-up calls to get the order by its ID or the order history for the customer.
