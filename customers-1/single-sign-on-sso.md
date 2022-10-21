---
description: Understand single sign-on.
---

# Single sign-on (SSO)

The Remote User Management service is a Digital River single sign-on (SSO) API for clients. The API allows end-users to sign on once and navigate across multiple domains. Clients can choose to pass user attributes that you can use to customize session management or order management.

{% hint style="info" %}
**Example:** You can customize the session management to target merchandising or customize order management to capture user attributes as part of the order.
{% endhint %}

When using SSO, you can assume the following:

* Digital River is the primary record for user information
* The client acts as a replica and updates user information from the primary as needed
* Digital River allows the creation of new users and sends the registration information to the primary for validation

Digital River sites contain a MyAccount section for self-service activities that allows you to manage accounts, orders, billing options, and subscriptions for end-users. With SSO in place, you can assume the following:

* User information updates go to a page hosted on a client site. The page can be either a pop-up page or a direct link with a return\_to URL.
* The Forgot Password link goes to a client site. (Usually a pop-up window.)
* Digital River pages perform the order, billing options, and subscription management.

The following image shows the high-level overview diagram.

![High-level overview diagram](https://files.readme.io/f0a8e2f-Remote\_User\_Management.png)

The following list describes the entire SSO process:

* A customer can either sign on to the site/offering at the client site or sign on at Digital River. Remote Login calls verify the login request.
* The client hosts the My Profile pages, where customers can update their email address and address book. The client can also collect additional information not required by Digital River.

{% hint style="info" %}
**Example:** Employee Identification Number (EIN), etc.
{% endhint %}

* Digital River hosts the My Payment Information and My Order History pages. The customer can update billing account information through Digital River and view order details.
* The Remote Login Request/Response occurs when a customer signs on through Digital River. This sign-on allows the customer to log in to Digital River and the client simultaneously.
* The Remote Session Validation Request contains a client-validated token. The Remote Session Validation Response passes the client's Unique Authenticating ID to Digital River as the External Reference ID.
* The Get User Profile Request/Response retrieves updated customer information from the client. The customer initiates the call when they sign on to Digital River, ensuring that Digital River has the most up-to-date information from the client.
* At the time of purchase, the Create User Request/Response validates the new customer accounts at the client site. When the customer creates a new account, the call to the client retrieves a new Unique Authenticating ID (External Reference ID) for the new customer account.

## Full SSO

Digital River only supports the full SSO implementation. The Digital River SSO solution consists of the following APIs:

* [Remote login](single-sign-on-sso.md#remote-login)
* [Remote user fetch](single-sign-on-sso.md#remote-user-fetch)
* [Remote session validation](single-sign-on-sso.md#remote-session-validation)
* [Remote user create](single-sign-on-sso.md#remote-user-create)

The default timeout on a Digital River-hosted site is 60 minutes. However, it can be customized on a per-site basis.

When a user clicks a Logout button, Digital River can redirect the user to a client-provided URL and pass a successful URL parameter. The client redirects the user to the URL value defined by the successful URL parameter to complete the logout operation. Digital River does not provide an XML-based logout API.

Digital River places a Forgot Password link on the website to a client-provided URL that allows a customer to change their password. Digital River does not support a Forgot Password API.

Digital River can integrate with a client-owned SSO API. This integration requires custom work.

The successful operation of SSO APIs requires reliable communication. The following list describes the default behavior when there are communication failures:

* **RemoteSessionValidation**—The user does not see an error message because the failure is transparent. The user session is not authenticated.
* **RemoteUserFetch**—The user does not see an error message because the failure is transparent. The user profile is not updated.
* **RemoteLogin**—User sees an error message. The error message typically prompts the user to retry the request.
* **RemoteCreateUser**—User sees an error message. The error message typically prompts the user to retry the request.

### Remote login

The remote login process validates a login operation on the Digital River-hosted store.

All SSO communication occurs using an HTTPS endpoint. For added security, Digital River can encrypt a password using a prearranged symmetric key.

The extended `attributes` element under the Remote Login Request/Response complex type allows you to pass custom information as a key/value pair. Passing custom information requires extra work.

The following image shows the Remote login (MyAccount) flow diagram.

![Remote login (MyAccount)](https://files.readme.io/511fec1-Remote\_User\_Management\_2.png)

The following image shows the Remote login (on check out) flow diagram.

![Remote login (on check out)](https://files.readme.io/2435a55-Remote\_User\_Management\_3.png)

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
	"LoginRequest": {
		"userKey": {
			"userID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"externalReferenceID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"companyID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"loginID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "demo@digitalriver.com"
			},
			"siteID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:UserKey"
		},
		"password": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"__text": "123123"
		},
		"extendedAttributes": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns3": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns3:ExtendedAttributesInfoArray",
			"_xsi:nil": "true"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Successful response" %}
{% code overflow="wrap" %}
```json
{
	"LoginResponse": {
		"successful": {
			"_xsi:type": "xsd:boolean",
			"__text": "false"
		},
		"errorCode": {
			"_xsi:type": "xsd:string",
			"__text": "5"
		},
		"errorMessage": {
			"_xsi:type": "xsd:string",
			"__text": "Invalid login"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:LoginResponse",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Unsuccessful response" %}
{% code overflow="wrap" %}
```json
{
	"LoginResponse": {
		"successful": {
			"_xsi:type": "xsd:boolean",
			"__text": "true"
		},
		"userKey": {
			"loginID": {
				"_xsi:type": "xsd:string",
				"__text": "demo@digitalriver.com"
			},
			"externalReferenceID": {
				"_xsi:type": "xsd:string",
				"__text": "D05B4D68-F49D-11DA-8019-88F835DA4C6C"
			},
			"siteID": {
				"_xsi:type": "xsd:string",
				"__text": "headwtr"
			},
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:UserKey",
			"__prefix": "ns2"
		},
		"extendedAttributes": {
			"item": {
				"name": {
					"_xsi:type": "xsd:string",
					"__text": "crmSession"
				},
				"value": {
					"_xsi:type": "xsd:string",
					"__text": "F3CB68D6-1643-11DD-8402-E6326E64542C/8443"
				},
				"valueDataType": {
					"_xsi:type": "xsd:string",
					"__text": "string"
				},
				"_xsi:type": "common:ExtendedAttributesInfo"
			},
			"_xmlns:common": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "common:ExtendedAttributesInfoArray",
			"__prefix": "common"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:LoginResponse",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Remote user fetch

Use Remote User Fetch to get additional user information. This call is available for those clients who want to provide separate APIs for fetching user information. This call allows Digital River to get the latest user profile information. The examples in this section depict the typical usage for this call.

When a user clicks a link to update their profile information on a Digital River-hosted store, they are redirected to a client site to complete their profile updates. When the user has finished updating their profile, the client uses a redirect to return the user to the Digital River-hosted page, where you can set up a real-time call to get the latest profile information. The Remote User Fetch allows both parties to have up-to-date user profile information.

All SSO communication occurs using an HTTPS endpoint. For added security, Digital River can encrypt a password using a prearranged symmetric key.

The extended `attributes` element under the Remote User Fetch Request/Response complex type allows you to pass custom information as a key/value pair. Passing custom information requires extra work.

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```json
{
	"GetUserProfileRequest": {
		"userKey": {
			"userID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"externalReferenceID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "D05B4D68-F49D-11DA-8019-88F835DA4C6C"
			},
			"companyID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "headwtr"
			},
			"loginID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"siteID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "headwtr"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:UserKey"
		},
		"sessionToken": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"_xsi:nil": "true"
		},
		"extendedAttributes": {
			"item": {
				"name": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "crmSession"
				},
				"value": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "F3CB68D6-1643-11DD-8402-E6326E64542C/8443"
				},
				"valueDataType": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"_xsi:type": "ns3:ExtendedAttributesInfo"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns3": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns3:ExtendedAttributesInfoArray"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Successful response" %}
{% code overflow="wrap" %}
```json
JSON{
	"GetUserProfileResponse": {
		"userInfo": {
			"userKey": {
				"loginID": {
					"_xsi:type": "xsd:string",
					"__text": "D05B4D68-F49D-11DA-8019-88F835DA4C6C"
				},
				"externalReferenceID": {
					"_xsi:type": "xsd:string",
					"__text": "D05B4D68-F49D-11DA-8019-88F835DA4C6C"
				},
				"siteID": {
					"_xsi:type": "xsd:string",
					"__text": "headwtr"
				},
				"_xsi:type": "ns2:UserKey"
			},
			"firstName": {
				"_xsi:type": "xsd:string",
				"__text": "Amit å"
			},
			"lastName": {
				"_xsi:type": "xsd:string",
				"__text": "Bartake ä"
			},
			"email": {
				"_xsi:type": "xsd:string",
				"__text": "abartake@digitalriver.com"
			},
			"homePhone": {
				"_xsi:type": "xsd:string",
				"__text": "9522538664"
			},
			"shippingAddress": {
				"name1": {
					"_xsi:type": "xsd:string",
					"__text": "Demo"
				},
				"name2": {
					"_xsi:type": "xsd:string",
					"__text": "Tester"
				},
				"line1": {
					"_xsi:type": "xsd:string",
					"__text": "1234 Test Avenue"
				},
				"line2": {
					"_xsi:type": "xsd:string"
				},
				"line3": {
					"_xsi:type": "xsd:string"
				},
				"city": {
					"_xsi:type": "xsd:string",
					"__text": "Eden Prairie"
				},
				"country": {
					"_xsi:type": "xsd:string",
					"__text": "US"
				},
				"countryName": {
					"_xsi:type": "xsd:string",
					"__text": "United States"
				},
				"postalCode": {
					"_xsi:type": "xsd:string",
					"__text": "55344"
				},
				"email": {
					"_xsi:type": "xsd:string",
					"__text": "demo@digitalriver.com"
				},
				"phoneNumber": {
					"_xsi:type": "xsd:string",
					"__text": "952-111-2222"
				},
				"_xsi:type": "ns2:AddressInfo"
			},
			"billingAddress": {
				"name1": {
					"_xsi:type": "xsd:string",
					"__text": "Demo"
				},
				"name2": {
					"_xsi:type": "xsd:string",
					"__text": "Tester"
				},
				"line1": {
					"_xsi:type": "xsd:string",
					"__text": "1234 Test Avenue"
				},
				"line2": {
					"_xsi:type": "xsd:string"
				},
				"line3": {
					"_xsi:type": "xsd:string"
				},
				"city": {
					"_xsi:type": "xsd:string",
					"__text": "Eden Prairie"
				},
				"country": {
					"_xsi:type": "xsd:string",
					"__text": "US"
				},
				"countryName": {
					"_xsi:type": "xsd:string",
					"__text": "United States"
				},
				"postalCode": {
					"_xsi:type": "xsd:string",
					"__text": "55344"
				},
				"email": {
					"_xsi:type": "xsd:string",
					"__text": "demo@digitalriver.com"
				},
				"phoneNumber": {
					"_xsi:type": "xsd:string",
					"__text": "952-111-2222"
				},
				"_xsi:type": "ns2:AddressInfo"
			},
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:UserInfo",
			"__prefix": "ns2"
		},
		"errorMessage": {
			"_xsi:type": "xsd:string"
		},
		"extendedAttributes": {
			"item": {
				"name": {
					"_xsi:type": "xsd:string",
					"__text": "hasAcceptedTermsNConditions"
				},
				"value": {
					"_xsi:type": "xsd:string",
					"__text": "yes"
				},
				"valueDataType": {
					"_xsi:type": "xsd:string",
					"__text": "string"
				},
				"_xsi:type": "common:ExtendedAttributesInfo"
			},
			"_xmlns:common": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "common:ExtendedAttributesInfoArray",
			"__prefix": "common"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:GetUserProfileResponse",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Unsuccessful response" %}
{% code overflow="wrap" %}
```json
{
	"GetUserProfileResponse": {
		"userInfo": {
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:nil": "true",
			"_xsi:type": "ns2:UserInfo",
			"__prefix": "ns2"
		},
		"errorMessage": {
			"_xsi:type": "xsd:string",
			"__text": "User not active"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/RemoteUserManagement/1.0",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:GetUserProfileResponse",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Remote session validation

An important element of a seamless single sign-on process is validating a remotely-authenticated user. Digital River initiates this process by searching the HTTP header for a predetermined cookie. This cookie is a remote session token that allows Digital River to contact the client and validate the user. Once Digital River validates the token and receives a corresponding authenticated user ID from the client, it instantiates an authenticated user session.

A session token is an encrypted key that is passed either as a cookie, an HTTP URL parameter, or through some other means. Digital River reads the token and uses it to create a Remote Session Validation call. You can pass multiple tokens as extended attributes of the Validate Session Request.

The extended `attributes` element under Validate Session Request/Response complex type allows you to pass custom information as a key/value pair. Passing custom information requires extra work.

{% tabs %}
{% tab title="Request sample (single token)" %}
```
demo@digitalriver.com D05B4D68-F49D-11DA-8019-88F835DA4C6C
```
{% endtab %}

{% tab title="Successful response sample (xsi:type is optional)" %}
{% code overflow="wrap" %}
```json
true demo@digitalriver.com D05B4D68-F49D-11DA-8019-88F835DA4C6C headwtr crmSession 
F3CB68D6-1643-11DD-8402-E6326E64542C/8443 string
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Remote user create

In the case where a customer never signs on and creates a new account during the checkout process, Digital River will forward the customer information to the client and then create a local user for that customer.

All SSO communication occurs using an HTTPS endpoint. For added security, Digital River can encrypt a password using a prearranged symmetric key.

The extended `attributes` element under the Create User Profile Request/Response complex type allows you to pass custom information as a key/value pair. Passing custom information requires extra work.

{% tabs %}
{% tab title="Payload" %}
```
demo@digitalriver.com DR Demo demo@digitalriver.com en_US 95888914269 
Minnetonka MN United States 10380 Bren Road W DR 
Demo 9522251234 55343 MN demo@digitalriver.com DR 123123
```
{% endtab %}

{% tab title="" %}
```
true D05B4D68-F49D-11DA-8019-88F835DA4C6C demo@digitalriver.com 
D05B4D68-F49D-11DA-8019-88F835DA4C6C crmSession 
F3CB68D6-1643-11DD-8402-E6326E64542C/8443 string
```
{% endtab %}

{% tab title="Unsuccessful response" %}
```
false 5 Email already used
```
{% endtab %}
{% endtabs %}

**Schemas**

| Version     | Schema Components Table                                                                      | Raw Schema                                                                       | Sample XML                                                                               |
| ----------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| 6 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RemoteUserManagement/6) | [View](https://drhadmin.digitalriver.com/integration/xsd/RemoteUserManagement/6) | [View](https://drhadmin.digitalriver.com/integration/isg/example/RemoteUserManagement/6) |
| 5           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RemoteUserManagement/5) | [View](https://drhadmin.digitalriver.com/integration/xsd/RemoteUserManagement/5) | [View](https://drhadmin.digitalriver.com/integration/isg/example/RemoteUserManagement/5) |
| 4           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RemoteUserManagement/4) | [View](https://drhadmin.digitalriver.com/integration/xsd/RemoteUserManagement/4) | [View](https://drhadmin.digitalriver.com/integration/isg/example/RemoteUserManagement/4) |
