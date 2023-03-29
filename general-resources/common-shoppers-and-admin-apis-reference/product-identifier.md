---
description: Understand the product identifier.
---

# Product identifier

A product identifier is the client's unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`. The product identifier value (`productID` or `PID`) is the identifier associated with a product.&#x20;

## Admin APIs and the product identifier

When you create a product programmatically or through [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), Digital River automatically assigns a product identifier to the product.&#x20;

The `productId` or `PID` variable can be one of the following values: an [individual](../admin-apis-reference/products.md#individual-product), [base](../admin-apis-reference/products.md#base-product), or product variation identifier. If you want to use your company's internal product identifiers, see [External reference identifier (ERID)](external-reference-identifier-erid.md) for instructions.

## Shopper APIs and the product identifier

You can use a product identifier to search for a product or add a product to a cart. The following examples demonstrate how you can use the product identifier (`id`) with the product-related resource. If you want to use your company's internal product identifiers, see [External reference identifier (ERID)](external-reference-identifier-erid.md) for instructions.

### Retrieve specific products from the default catalog

The following request gets a product by its product identifier of `64578500`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 
'https://api.digitalriver.com/v1/shoppers/me/products?id=64578500' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Add a product to a shopping cart using the external reference identifier

The following request example adds a product to a cart using the `id` query parameter.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-json" data-overflow="wrap"><code class="lang-json">curl --location --request GET 
<strong>'https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?id=64578500' \
</strong>--header 'Authorization: Bearer &#x3C;API_key>' \
...
</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you do not provide a company identifier, The API uses the company identifier associated with the API key.
{% endhint %}

### Add a product by external reference identifier to the shopping cart and redirect to the storefront page

In a typical anonymous customer workflow, you can add products to a cart by external reference identifier, making a single POST call with a payload to the [Web Checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout) resource. The following payload (request entity) adds a product with the `id`of `64578500`, with a `quantity` of `2`, to a cart.

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" %}
```json
 {
   "webCheckout": {
     "cart": {
       "lineItems": {
         "lineItem": {
           "quantity": "2",
           "product": {
             "idd": "64578500"
            }
              ... more closing curly braces ...
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful request with this particular API results in a `302 redirect` to a Digital River-hosted guest checkout page.&#x20;
