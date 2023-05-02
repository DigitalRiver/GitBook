---
description: Learn about the client-maintained customer login.
---

# Client-maintained customer login

If you maintain the master record for the customer login credentials, the payload must contain the `externalReferenceId`.

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" %}
```json
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
{% endcode %}
{% endtab %}
{% endtabs %}

The response returns an HTTP Status 201 Created from the server.

After you create a base customer record, you can get an authenticated customer token and call the `GET shoppers/me/account` resource to allow the customer to log in and configure their account information. The account information associated with a customer includes the shipping address, billing address, and payment options.
