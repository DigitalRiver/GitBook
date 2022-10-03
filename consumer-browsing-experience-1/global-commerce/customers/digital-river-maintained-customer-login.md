---
description: Learn about the Digital River-maintained customer login.
---

# Digital River-maintained customer login

If Digital River maintains the master record for the customer login credentials, the request body must contain the `username` and `password`. The customer's `password` must be base64 encoded.

{% hint style="info" %}
**Best Practices**: Explicitly set the `locale` and `currency` for a customer at the start of a session.
{% endhint %}

{% tabs %}
{% tab title="Example" %}
```javascript
{
	"shopper": {
		"username": "myShopper@myCompany.com",
		"password": "cFGzc3dvcmQ=",
		"firstName": "John",
		"lastName": "Johnson",
		"emailAddress": "jjohnson@myCompany.com",
		"locale": "en_US",
		"currency": "USD"
 	}
 }
```
{% endtab %}
{% endtabs %}
