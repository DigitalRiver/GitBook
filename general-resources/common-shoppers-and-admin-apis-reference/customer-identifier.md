---
description: Understand the customer identifier.
---

# Customer identifier

The Remote User Management (also known as SSO) service requires an `externalReferenceID` as a customer identifier.&#x20;

{% hint style="danger" %}
You must specify a unique `externalReferenceID` for each user because several objects use it. Failure to do so may violate your contract with Digital River and will cause users to get cross-linked.&#x20;
{% endhint %}

You must specify a unique inbound `userKey` (in response to `LoginRequest`, `GetUserRequest`) for each user in the clients' database.

## Using an external reference identifier for a customer

When you create a customer, you can specify the external reference ID. You can also update a customer using the [`POST /shoppers/me`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post) resource.

### Specifying an external reference identifier when creating and getting a customer

The shopper object in the payload for a [`POST /shoppers`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers/post) request (where the client maintains the login credentials) includes an `externalReferenceId` as shown in line 5:

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" lineNumbers="true" %}
```json
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

When you use the [`GET /shoppers/me`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/get) resource to get a customer, you can use the `expand` query parameter to get the customer's external reference identifier. Note that the GET does not return the external reference identifier field by default. For more information about getting and creating customers, refer to the [Shopper ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers)resource.

### Create a full access token using the external reference identifier

For the Client Credentials confidential flow only, you can create a full access token on behalf of a customer by passing in the `external_reference_id` form parameter in the payload:

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" %}
```http
grant_type=client_credentials&amp;dr_external_reference_id=partner-shopper-id
```
{% endcode %}
{% endtab %}
{% endtabs %}

For more information, see [`POST oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) under the [Token API](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token).
