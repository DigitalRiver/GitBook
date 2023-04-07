---
description: Learn how to use fields as keys.
---

# Fields used as keys

You can use the following keys described below with Order Notification, Sales Order Activity, and Subscription Services for reporting purposes.

## Email address

To use email as a key, check the `email` element under the `billingAddress` element first.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"billingAddress": {
		"emailAddress": ""
	}
}
```
{% endtab %}
{% endtabs %}

If no `billingAddress` elements exist, locate the `email` element associated with the `shippingAddress`**.**

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"shippingAddress": {
		"emailAddress": ""
	}
}
```
{% endtab %}
{% endtabs %}

Any `shippingAddress` for any `lineItem` will suffice since the address appears for all the line items.

## Consumer name

To use the consumer name as a key, check the `name` element under the `payment` element first.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"payment": {
		"customerFirstName": "",
		"customerLastName": ""
	}
}
```
{% endtab %}
{% endtabs %}

If no `payment` element exists, locate the consumer `name` element associated with the `shippingAddress`.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"shippingAddress": {
		"customerFirstName": "",
		"customerLastName": ""
	}
}
```
{% endtab %}
{% endtabs %}

Any the `shippingAddress` for any `lineItem` will suffice since the address appears for all the line items.

## Digital rights

To use digital rights as a key, check the `serialNumber` and `unlockCode` elements under the `lineItems` element.

{% tabs %}
{% tab title="Plain Text" %}
```javascript
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
{% endtab %}
{% endtabs %}

## CustomerID field

Use the `customerID` field as a key, when you want to attribute orders to users who have access to MyAccount where they can change their login IDs and email addresses.