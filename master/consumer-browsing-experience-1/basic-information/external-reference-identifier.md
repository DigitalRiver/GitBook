---
description: Learn how to use the external reference identifier.
---

# External reference identifier

You can use an external reference ID (`externalReferenceID`) to reference either a customer or a product owned by a Digital River client.&#x20;

## Customer identifier

The Remote User Management (also known as SSO) service requires an `externalReferenceID`. You must specify a unique `externalReferenceID` for each user because several objects use it. Failure to do so may violate your contract with Digital River and will cause users to get cross-linked. You must specify a unique inbound `userKey` (in response to `LoginRequest`, `GetUserRequest`) for each user in the clients' database.

### Using an external reference identifier for a customer

When you create a customer, you can specify the external reference ID. You can also update a customer using the [`POST /shoppers/me`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post) resource.

#### Specifying an external reference identifier when creating and getting a customer

The Shopper object in the request body for a [`POST /shoppers` ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers/post)request (where the client maintains the login credentials) includes an `externalReferenceId` as shown in line 5:

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```javascript
{
 		"shopper": {
 			"firstname": "John",
			"lastname": "Johnson",
 			"externalreferenceid": "abc123",
 			"emailaddress": "jjohnson@myCompany.com",
 			"locale": "en_US",
 			"currency": "USD"
	 	}
 }
```
{% endcode %}
{% endtab %}
{% endtabs %}

When you use the [`GET /shoppers/me`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/get) resource to get a customer, you can use the `expand` query parameter to get the customer's external reference identifier. Note that the GET does not return the external reference identifier field by default. For more information about getting and creating customers, refer to the [Shopper ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resource.

#### Create a full access token using the external reference identifier

For the Client Credentials confidential flow only, you can create a full access token on behalf of a customer by passing in the `external_reference_id` form parameter in the request body (payload):

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```
grant_type=client_credentials&amp;dr_external_reference_id=partner-shopper-id
```
{% endcode %}
{% endtab %}
{% endtabs %}

For more information, see [`POST oauth20/token`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) under the [Token API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token).

## Product identifier

A product identifier is assigned when someone creates a product in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Some companies have their internal identifiers for their products, and that external reference ID may or may not match the product identifier in Global Commerce. You can search for and add products to a cart based on either the external reference identifier or product ID as you prefer. The following examples demonstrate various ways you can use the external reference ID with the product-related [Shopper ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resource.

### Retrieve products from the default catalog, limited by specific external reference identifiers

The following request gets products with an `externalReferenceId` of `30`, `35`, and `40`.

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```
GET shoppers/me/products?externalReferenceId=30,35,40
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Add a product to a shopping cart using the external reference identifier

The following request example adds a product to a cart using the `externalReferenceId` query parameter.

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```
POST shoppers/me/carts/active/line-items?externalReferenceId=0123456789
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you do not provide a company identifier, The API uses the company identifier associated with the API key.
{% endhint %}

### Add a product by external reference identifier to the shopping cart and redirect to the storefront page

In a typical anonymous customer workflow, you can add products to a cart by external reference identifier, making a single POST call with a payload to the [Web Checkout](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Web-Checkout) resource. The following payload (request entity) adds a product with the `externalReferenceId` of `123456789`, with a `quantity` of `2`, to a cart.

{% tabs %}
{% tab title="Payload sample" %}
{% code overflow="wrap" %}
```javascript
 {
   "webCheckout": {
     "cart": {
       "lineItems": {
         "lineItem": {
           "quantity": "2",
           "product": {
             "externalReferenceId": "123456789"
            }
              ... more closing curly braces ...
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful request with this particular API results in a 302 redirect to a Digital River-hosted guest checkout page. For more information, see [Create the cart and transfer shopper](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Web-Checkout/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1web-checkout/post).
