---
description: >-
  Learn how to add the information required to support a specific payment
  method.
---

# Adding required information for specific payment methods

Specific payment methods such as [TreviPay ](../../payments/payments-solutions/digitalriver.js/payment-methods/trevipay.md)require the organization identifier (`organizationId`).  For example, use the value associated with TreviPay's `client reference_id` as the value for the `organizationId`. The following instructions show you how to add or remove the organization identifier.

## Adding an organization identifier to a cart

You can add a shopper's organization identifier when you update a cart. We pass the organization identifier to the payment session where the payment method becomes available.&#x20;

Use the [`POST /shoppers/me/carts/active`](https://drapi.io/commerce/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) resource to add an `organizationId` to the cart.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/shoppers/me/carts/active' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
		"cart": {
				"organizationId": "Acme_Inc",
				"lineItems": {
						"lineItem":
								{
										"quantity": "1",
										"product": {
												"id": "5326162000"
										}
								}
				}
			}
}'
```
{% endtab %}
{% endtabs %}

A successful request returns a `200 OK` response.

{% tabs %}
{% tab title="200 OK response" %}
```javascript
{
  "cart": {
    ...
    "organizationId": "Acme_Inc"
  }
}
```
{% endtab %}
{% endtabs %}

## Removing an organization identifier from the cart

Use the [`POST /shoppers/me/carts/active`](https://drapi.io/commerce/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) resource and an empty `organizationId` string to delete the organization identifier from the cart.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/shoppers/me/carts/active' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
		"cart": {
				"organizationId": "",
				"lineItems": {
						"lineItem":
								{
										"quantity": "1",
										"product": {
												"id": "5326162000"
										}
								}
				}
			}
}'
```
{% endtab %}
{% endtabs %}

A successful request returns a `200 OK` response.

{% tabs %}
{% tab title="200 OK response" %}
```javascript
{
  "cart": {
    ...
  }
}
```
{% endtab %}
{% endtabs %}

