---
description: Learn about the client-maintained customer login.
---

# Client-maintained customer login

If the client (that is, customer) maintains the master record for the customer login credentials, the request body must contain the `externalReferenceId`.

{% tabs %}
{% tab title="Example" %}
```javascript
{
	"shopper": {
		"firstName": "John",
		"lastName": "Johnson",
		"externalReferenceId": "abc123",
		"emailAddress": "jjohnson@myCompany.com",
		"locale": "en_US",
		"currency": "USD"
	 }
 }
```
{% endtab %}
{% endtabs %}

The response returns an HTTP Status 201 Created from the server.

After you create a base customer record, you can get an authenticated customer token and call the `GET shoppers/me/account` resource to allow the customer to log in and configure his or her account information. The account information associated with a customer includes shipping address, billing address, and payment options.
