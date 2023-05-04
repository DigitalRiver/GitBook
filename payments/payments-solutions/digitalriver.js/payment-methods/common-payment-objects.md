---
description: Learn about payment objects that are common to all payment methods.
---

# Common payment objects

## Owner object

{% tabs %}
{% tab title="Owner object example" %}
{% code overflow="wrap" %}
```javascript
{
	"firstName": "Otis",
	"lastName": "Lin",
	"email": "test@digitalriver.com",
	"phoneNumber": "01314532211",
        "organization": "DR",
	"address": {
	  "line1": "东城区景山前街4号",
	  "city": "北京市",
	  "country": "CN",
	  "postalCode": "100009"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Field                 | Required/Optional | Description                                                                                                                                                                                               |
| --------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| firstName             | Required          | The customer's first name as it appears on the payment instrument.                                                                                                                                        |
| lastName              | Required          | The customer's last name as it appears on the payment instrument.                                                                                                                                         |
| phoneNumber           | Required          | The customer's phone number.                                                                                                                                                                              |
| email                 | Required          | The customer's email address.                                                                                                                                                                             |
| address               | Required          | An [Address object](common-payment-objects.md#address-object).                                                                                                                                            |
| additionalAddressInfo | Optional          | <p>An <a href="common-payment-objects.md#additional-address-information-object">Additional Address Information object</a>.</p><p>Additional address fields may be required for certain payment types.</p> |

## Address object

{% tabs %}
{% tab title="Address object example" %}
{% code overflow="wrap" %}
```javascript
{
	"line1": "1-16-24 Minami-gyotoku",
	"line2": "Ichikawa-shi",
	"city": "Chiba",
	"state": "Kyongsangnamdo",
	"postalCode": "272-0138",
	"country": "JP"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Field      | Required/Optional | Description                                    |
| ---------- | ----------------- | ---------------------------------------------- |
| line1      | Required          | Line 1 of the Customer's billing address.      |
| line2      | Required          | Line 2 of the Customer's billing address.      |
| city       | Required          | City of the Customer's billing address.        |
| state      | Required          | State of the Customer's billing address.       |
| postalCode | Required          | Postal Code of the Customer's billing address. |
| country    | Required          | Country of the Customer's billing address.     |

## Additional address information object

{% tabs %}
{% tab title="Additional Address Information object" %}
{% code overflow="wrap" %}
```javascript
{
    "neighborhood": "Centro",
    "phoneticFirstName": "John",
    "phoneticLastName": "Doe",
		"division": "Development"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Field             | Required/Optional | Description                                         |
| ----------------- | ----------------- | --------------------------------------------------- |
| neighborhood      | Optional          | The neighborhood of the Customer.                   |
| phoneticFirstName | Optional          | The phonetic spelling of the Customer's first name. |
| phoneticLastName  | Optional          | The phonetic spelling of the Customer's last name.  |
| division          | Optional          | The division applicable to the Customer.            |

