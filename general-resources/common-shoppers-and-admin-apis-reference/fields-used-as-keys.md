---
description: Learn how to use fields as keys.
---

# Fields used as keys

You can use the following keys described below with Order Notification, Sales Order Activity, and Subscription Services for reporting purposes.

## Email address

To use email as a key, check the `emailAddress` element under the `billingAddress` element first.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
	"billingAddress": {
		"emailAddress": ""
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

If no `billingAddress` elements exist, locate the `emailAddress` element associated with the `shippingAddress`**.**

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
	"shippingAddress": {
		"emailAddress": ""
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Any `shippingAddress` for any `lineItem` will suffice since the address appears for all the line items.

## Consumer name

To use the consumer name as a key, check the `name` element under the `payment` element first.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
	"payment": {
		"customerFirstName": "",
		"customerLastName": ""
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

If no `payment` element exists, locate the consumer `name` element associated with the `shippingAddress`.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
	"shippingAddress": {
		"customerFirstName": "",
		"customerFastName": ""
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Any the `shippingAddress` for any `lineItem` will suffice since the address appears for all the line items.

## Digital rights

To use digital rights as a key, check the `serialNumber` and `unlockCode` elements under the `lineItems` element.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
	"lineItems": {
		"lineItem": {
			"digitalRights": {
				"serialNumber": "",
				"unlockCode": ""
			}
		}
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## CustomerID field

Use the `customerID` field as a key, when you want to attribute a [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/retrieveSources)or order to a shopper who has access to MyAccount where they can change their login ID, email address, and payment method.
