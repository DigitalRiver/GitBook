---
description: Understand the Commerce API structure.
---

# API structure

The Commerce API and the Product Admin API is a [RESTful API](https://restfulapi.net/). We designed the API to allow you to create, read, update, and delete objects with the`POST`, `GET`, `PUT` and `DELETE` [HTTP methods](https://www.restapitutorial.com/lessons/httpmethods.html).

The Commerce API and the Product Admin API speak exclusively in [JSON](https://www.json.org/json-en.html). To ensure the API accepts and processes your requests, always set the `Content-Type` header to `application/json` .

All Commerce API and Product Admin API requests are sent to `https://api.digitalriver.com`.

For more information on how Digital River ensures high availability and performance, see our [Service Level Agreement](https://www.digitalriver.com/legal-information/).

## API keys

Digital River uses your account's API keys to authenticate your API requests. If you do not include your key when you send an API request or use an incorrect or outdated key, Digital River returns an error.

Your account provides separate keys for testing and for running live transactions. You can use these keys when sending API requests in either test or live mode. Resources in one mode cannot change resources in another mode.

{% hint style="success" %}
We recommend a separate set of API keys for the Commerce API and Product Admin API.
{% endhint %}

### Public keys

The public API keys identify your account with Digital River and allow you to create sources. You can use them with your [DigitalRiver.js](https://docs.digitalriver.com/commerce-api/payment-integrations-1/digitalriver.js) JavaScript code.&#x20;

### **Private keys**

The private (secret) API keys allow you to send an API request to Digital River without restriction. Keep these keys confidential and only store them on your servers. Don't use your confidential key for everything.

## Authentication

The Commerce API authenticates and Product Admin API requests using API keys. Contact your Account Manager to obtain your API keys.

The Commerce API and Product Admin API use OAuth for authentication. OAuth is an open protocol that provides secure authorization for web, mobile, and desktop applications. A third-party application can use the OAuth 2.0 authorization framework to obtain limited access to an HTTP service.

{% hint style="success" %}
Use the OAuth 2.0 authentication exclusively with the Commerce APIs. For Product Admin API, you can use either a [secret key](API-structure.md#private-keys) or a [Global Commerce access token](../product-admin-api/administrator-browser-experience/product-basics/global-commerce-access-token.md). We recommend using the [secret key](API-structure.md#private-keys) with the Product Admin API because the Global Commerce access token will expire in one day by default. The `expires_in` value determines when the access token will expire. You will have to request a new access token when the current access token expires.
{% endhint %}

The Commerce API and Product Admin API use the OAuth 2.0 W3C (World Wide Web Consortium) standard to authenticate and authorize shoppers and their data. OAuth 2.0 allows you, the developer, to access a shopper's account without requiring shoppers to share their account credentials (username and password).

**Consumer-facing applications**—Use OAuth to publish and interact with protected data when you are building:

* Web
* Desktop
* Mobile
* Web page widgets
* JavaScript
* Browser-based applications

**Service Providers**—Use OAuth to give users access to their data while protecting their account credentials when:

* Supporting the web and mobile applications
* Supporting server-side API mashups
* Storing protected data on behalf of your users

### Authorize shopper

Applications use the /oauth20/authorize API to create an authenticated shopper token for a shopper. This API call results in a 302 response that you can use to direct the user to an identity provider (IDP)-hosted login page. After the shopper successfully signs in, a redirect Uniform Resource Identifier (URI) query parameter returns control to the application. The URI query parameter contains an authenticated shopper token parameter that you can use to make subsequent API calls.

The workflow that an application should implement depends on the type of client, which can be Public.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
GET /oauth20/authorize?redirect_uri=http%253A%252F%252Fexample.com&client_id=a78b756bd47e258841d7f007f3f62a&response_type=token&dr_limited_token=6c6bfd0fb07be35c608a2b8e5f5ae72e
```
{% endcode %}
{% endtab %}

{% tab title="HTTP" %}
{% code overflow="wrap" %}
```http
Host: api.digitalriver.com
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_102)
Accept: application/json (Default)

```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
{% code overflow="wrap" %}
```typescript
The request body should be empty. 
```
{% endcode %}
{% endtab %}

{% tab title="HTTP" %}
```http
HTTP/1.1 200 OK
Content-Length: 161
Access-Control-Allow-Origin: *
```
{% endtab %}

{% tab title="JSON" %}
```javascript
The response body should be empty.
```
{% endtab %}
{% endtabs %}

### Token

Use the `/oauth20/token` resource to generate either an [anonymous or authenticated shopper token](API-structure.md#about-oauth-access-tokens). You can also use it to refresh an access token. The API requirements depend on the type of application that invokes a request.

The `/oauth20/token` resource generates an access token that you can use to access resources. A shopper can use an anonymous shopper token to anonymously shop for a product. You need an authenticated shopper token to retrieve authenticated shopper-specific details, such as address or payment details. This token only supports a public workflow.

See [Create a Token](https://commerceapi.digitalriver.com/reference#oauth20tokenclientcredentialspost) for more information.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
POST /oauth20/token
```
{% endcode %}
{% endtab %}

{% tab title="Request Headers" %}
{% code overflow="wrap" %}
```
Host: api.digitalriver.com
User-Agent: API Client/1.0
Accept: application/json (Default)
Authorization: Basic username: client id password: client secret
```
{% endcode %}
{% endtab %}

{% tab title="Request Body" %}
{% code overflow="wrap" %}
```
grant_type=client_credentials&dr_external_reference_id=partner-shopper-id

```
{% endcode %}
{% endtab %}

{% tab title="Response Headers" %}
{% code overflow="wrap" %}
```
HTTP/1.1 200 OK
Content-Length: 161
Access-Control-Allow-Origin: *
```
{% endcode %}
{% endtab %}

{% tab title="Response Body" %}
{% code overflow="wrap" %}
```
				
{
   "access_token": "your_access_token",
   "token_type": "bearer",
   "expires_in": "3599",
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

### Initiate an authenticated session

Send the following request to create an anonymous shopper token to identify the shopper session:

{% code title="Request Sample" overflow="wrap" %}
```http
POST https://api.digitalriver.com/oauth20/token.json
```
{% endcode %}

Include your base64-encoded API key and secret in the request header. Include `grant_type=client_credentials` and the `externalReferenceId` in the request body.

This Token API identifies a shopper session and consists of an `access_token` and a `refresh_token`. They correspond to the session cookie and the browser cookie. You can save the `access_token` and `refresh_token` in the application and use them in subsequent queries. The `access_token` expires after a specified interval (60 minutes by default in user session site settings in Digital River. The `refresh_token` expires after one year.

The `expires_in` property is the time-to-live (TTL) value for the access token. You can refresh the access token at any time.

### OAuth 2.0 APIs

Digital River uses OAuth 2.0 to provide authentication and authorization for the Commerce APIs. The Digital River OAuth 2.0 API allows third-party applications to authenticate and perform actions on behalf of a shopper without acquiring the shopper's password. Public resources do not require an access token, but they do require an API key configured as a public key.

You can invoke various OAuth APIs and sequences of API calls to implement the OAuth workflows.

You can implement the OAuth 2.0 APIs workflows using the following resources:

* /oauth20/token
* /oauth20/authorize

Use the /oauth20/token API to establish an anonymous shopper (limited access) token. You can use the anonymous shopper token to access resources before shopper authentication. You must provide your API key as a query parameter when you request an access token from the oauth20/token resource.

![Anonymous Shopper Token](https://files.readme.io/b77d813-Oauth\_2.0-01.png)

The **anonymous shopper token** is an authenticated token, but not an authorized token. You can use the `/oauth20/authorize` resource to authenticate a shopper and establish an authenticated shopper token. An authenticated shopper token allows an application to use all of the shoppers/me APIs. You must send a request to the `oauth20/authorize` resource that includes:

* Your API key or access token as a query parameter
* The redirect URI sends the shopper to the correct page after the shopper successfully signs in

This request redirects the shopper to the Global Commerce platform for authentication. After the shopper successfully signed in, the system redirects the shopper to the specified URI and adds the new authenticated token as a parameter.

![Authenticated Shopper Token](https://files.readme.io/437002b-Oauth\_2.0\_b-01-01.png)

In this instance, the full access token replaces the limited access token, and future requests will use the full access token.

The OAuth 2.0 API uses application/json format by default.

#### About OAuth access tokens

OAuth is an open standard for authorization. OAuth allows users to share their private resources stored on one site with another site without submitting their user credentials. Each token grants access to a specific site for specific resources and a defined duration. This allows a user to grant third-party site access to the information they provided to another service provider without sharing their access permissions or the full extent of their data.

Digital River Connect APIs grant the following OAuth token types:

* **Anonymous shopper token**—A token that allows a shopper to access the Commerce APIs that do not require a consumer context. This token allows the shopper to send API requests against resources that are not shopper-protected. An anonymous shopper token is an authenticated token. However, it is not an authorized token that provides full access.
* **Authenticated shopper token**—A token that allows the shopper to access all Commerce APIs features. You can only get an authenticated shopper token when the shopper explicitly allows your application to access their data. Only the shopper can grant this token. To get an authorized token, you need to send the shopper to the Digital River platform for authentication. Your application has access to the full API after a shopper enters their credentials and explicitly grants your application permission to access their protected resources.

#### Valid token types

The [OAuth specification](https://tools.ietf.org/html/rfc6749) defines the available application type as follows:

* **Public applications**—Applications that are incapable of maintaining the confidentiality of their credentials or securely authenticating by any other means. All calls use an HTTP Basic Authentication header, with the client ID (API key) as the username, and never use the secret key.
* **Confidential applications**—Applications that are capable of maintaining the confidentiality of their credentials, or are otherwise capable of secure client authentication. All calls include an HTTP Basic Authentication header. The header contains the client ID (API key) as the username and the secret key as the password.

#### Access Token TTL

The access token time-to-live (TTL) limits the lifespan of the access token in seconds. When using TTL, consider the following:

* The default value is 24 hours (86397 seconds)
* By default, tokens remain valid for the same duration as Digital River-hosted storefront pages

The `expires_in` property is the TTL value for the access token. An application can store a valid access token and re-use it until it expires.

#### Public versus confidential authentication flows

**Public flow**

Your API key and OAuth tokens (both anonymous and authenticated) are obfuscated yet publicly available with the technical effort that likely takes some time. Use this flow only when replay attacks are unlikely within the span of the token lifetime and when the API key and tokens are obfuscated (such as behind a decompiler).

![Public Authentication Flow](https://files.readme.io/9a25c95-Oauth\_2.0\_cont.png)

**Confidential flow**

Your API key remains completely hidden from public view. You can obfuscate or hide OAuth anonymous tokens from public view. The OAuth authenticated token is fully hidden from the public and typically hidden via a server proxy between the application and Digital River servers.

![Confidential Authentication Flow](https://files.readme.io/14e138b-Oauth\_2.0\_cont\_b.png)

#### OAuth flows allowed by grant and client types

The following table shows the OAuth flows allowed by grant type and client type (including the application type). The table also indicates support for refresh tokens.

| Grant Type         | Public Application | Confidential Application | Refresh Token Supported? |
| ------------------ | ------------------ | ------------------------ | ------------------------ |
| Implicit           | Yes                | No                       | No                       |
| Client Credentials | No                 | Yes                      | No                       |
| ROPC               | Yes                | Yes                      | Yes                      |

See [Public vs. confidential application flows](API-structure.md#public-versus-confidential-authentication-flows) for more information.

### Creating session-aware access tokens

The session-aware access token links a Global Commerce shopper session to an access token as well as provide the ability to continue a shopper workflow with a previously established shopper session.

To create a session-aware access token, use the `sessionToken` query parameter or `dr_session_token` form parameter, depending on the workflow.

{% hint style="warning" %}
You **must** provide a session-aware token when transitioning a shopper from a 3rd-party application to a Digital River-hosted checkout experience to complete an online purchase.
{% endhint %}

You can create a session-aware token by either sending a browser call or a request to the **Token endpoint** in either the [Shopper API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers) or the [OAuth API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token).

{% hint style="info" %}
If you provide a session token when generating an access token, the system creates a new shopper session.
{% endhint %}

You can choose one of the following options to create a session-aware access token:

* ****[**Option 1**. Anonymous shopper token with an API key](API-structure.md#option-1-anonymous-shopper-token-with-an-api-key)
* ****[**Option 2**. Anonymous shopper token via Oauth 2.0](API-structure.md#option-2-anonymous-shopper-token-via-oauth-2-0)

#### **Option 1**: Anonymous shopper token with an API key

Establish an anonymous shopper (limited access) token in a single call by passing in your API key to the `sessionToken` site action.

{% tabs %}
{% tab title="Request Sample" %}
{% code overflow="wrap" %}
```
GET https://{store domain}/store/{SiteID}/SessionToken?apiKey={PublicAPIKey}
&format=json
```
{% endcode %}
{% endtab %}

{% tab title="Response Sample (session aware access token)" %}
{% code overflow="wrap" %}
```
{
  "token": {
    "access_token": 
"96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b52b...",
    "token_type": "bearer",
    "expires_in": "86397",
    "refresh_token": 
"96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b8f5..."
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
You must include the `sessionToken` site action. The `sessionToken` site action **MUST** come from the client side (the shopper's browser). You can do this via ajax and as shown in the following example.
{% endhint %}

{% code title="Example" overflow="wrap" %}
```
function sessionToken() {
       $.ajax({
          url: "https://store.digitalriver.com/store/[siteID]/SessionToken?apiKey=[apiKey]]&format=json",
           type: 'GET',
           async: false,
           contentType: "application/json",
           dataType: "jsonp",
            error: function (data) {
            },
            success: function (data) {
             }
        });
}
```
{% endcode %}

#### **Option 2**: Anonymous shopper token via Oauth 2.0

This example requires two calls; one to get the session token, and another to create the access token.

**Step 1: Get a dr\_session\_token from the `sessionToken` site action with no API key**

{% tabs %}
{% tab title="Request Sample" %}
{% code overflow="wrap" %}
```
GET https://{store domain}/store/{SiteID}/SessionToken?format=json
```
{% endcode %}
{% endtab %}

{% tab title="Response Sample" %}
{% code overflow="wrap" %}
```
{
  "session_token": "1A9C61A6B8B54BD7087A5AD8986A17FA"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
You must include the `sessionToken` site action and it **MUST** come from the client-side (the shopper's browser). You can do this via ajax, as shown in the following example.
{% endhint %}

{% code title="Example" overflow="wrap" %}
```
function sessionToken() {
       $.ajax({
          url: "https://store.digitalriver.com/store/[siteID]/SessionToken?apiKey=[apiKey]]&format=json",
           type: 'GET',
           async: false,
           contentType: "application/json",
           dataType: "jsonp",
            error: function (data) {
            },
            success: function (data) {
             }
        });
}
```
{% endcode %}

**Step 2: POST the dr\_session\_token to the oauth20 resource, to get an anonymous shopper token.**

{% tabs %}
{% tab title="Request Sample" %}
{% code overflow="wrap" %}
```
POST http://api.digitalriver.com/oauth20/token
```
{% endcode %}
{% endtab %}

{% tab title="Headers Sample" %}
{% code overflow="wrap" %}
```
Content-Type: application/x-www-form-urlencoded
Authorization: Basic NTcwZjg0YTg3OTM5NDI1ZThlMTFlZTEyMGRlMDc1ZGI6YmRhNjg5ODViZjI3NDJlOGFiYmVmNjhiYWU3YjRiNzU=
```
{% endcode %}
{% endtab %}

{% tab title="Body (url encoded) Sample" %}
{% code overflow="wrap" %}
```
dr_session_token: [from step #1)
grant_type: password
format:json
```
{% endcode %}
{% endtab %}

{% tab title="Response Sample" %}
{% code overflow="wrap" %}
```
{
  "token": {
    "access_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b52b...",
    "token_type": "bearer",
    "expires_in": "86397",
    "refresh_token": "96c44081d5ee98a7545ede88de966f0f371112b939b503219575572b5054be5b8f5..."
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The time-to-live (TTL) value for `expires_in` respects the user session site settings in Global Commerce. In this example, the token for the site expires in 86397 seconds (24 hours).
{% endhint %}

## Sending API calls using /auth

To use the Refunds or Sites resource, you need:

* A client ID or API key. You must specify either an API Key or a token.
* A customer's ID. You must specify either an API Key or a token.
* A Global Commerce admin username and password. The password should be base-64 encoded when authenticating.&#x20;
* The following table shows the Global Commerce roles (permissions) required for each resource:

| Role (Permissions)              | Resource |
| ------------------------------- | -------- |
| Customer Service Director       | Refunds  |
| Customer Service Representative | Refunds  |
| Customer Service Supervisor     | Refunds  |
| Site Manager                    | Sites    |

When a [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) user sends a call, they must supply their API key with `/auth`. The `/auth` must include the user's username and an encoded password for Global Commerce.&#x20;

{% hint style="info" %}
**Hint**: You will need your Global Commerce user credentials when you use the Refunds API or Sites API. For example, when using a Postman Collection you will need to provide these credentials in the  `csrUserName` and `csrPassword` fields.
{% endhint %}

When a Global Commerce user sends a call:

1. The Global Commerce user uses the API key when calling `/auth` and provides their Global Commerce account credentials (username and password).&#x20;
2. Global Commerce authenticates the credentials.

{% hint style="info" %}
**Example**: An external Global Commerce user with the Site Manager role can access the `/auth` service to get the `access_token` and then use that `access_token` to [get the authorized billing countries](../master/sites/getting-a-sites-authorized-billing-countries.md) and [authorized shipping countries](../master/sites/getting-a-sites-authorized-shipping-countries.md) from the Configure Site Setting page in Global Commerce.
{% endhint %}

{% tabs %}
{% tab title="POST /auth" %}
{% code overflow="wrap" %}
```javascript
{
    "access_token": "your_access_token",
    "token_type": "bearer",
    "expires_in": "3599"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Creating authenticated shopper tokens

Use the `GET /oauth20/authorize` resource to initiate the creation of an authenticated shopper (full access) token. This resource will return a 302 response that you can use to direct the user to an IDP-hosted login page. After the shopper logs in successfully, control returns to your application through the use of the redirect URI query parameter, which contains a full access token parameter that you can use to make subsequent API calls.

The workflow that an application should implement depends on the type of client, which can be **Public**.

{% hint style="info" %}
You can include an anonymous shopper (limited access) token as a query parameter to transition the shopper state to the authenticated shopper (full access) token.
{% endhint %}

## Mini cart widget

You can create a Mini Cart widget using javascript that runs on your website. The widget displays the contents of the cart to the shopper. You can choose to implement the Mini Cart widget with a public API key or a confidential API key. The Mini Cart widget initiates the Shopping API requests directly from a web browser using JSONP as the cross-domain solution. The Shopping APIs also support CORS.

The Mini Cart widget uses the following common Shopping APIs:

* `GET /oauth20/token`
* `POST v1/shoppers/me/carts/active?productId={​pid}​&quantity={​qty}`​&#x20;
* `POST v1/shoppers/me/carts/active/line-items?productId={​pid}​&quantity={​qty}`
* `GET v1/shoppers/me/carts/active`
* `POST v1/shoppers/me/carts/active/web-checkout`

## Custom attributes

You can enrich your product catalog data by providing custom attributes for one or all products in your Digital River catalog. Common attributes describe a product, such as size, color, platform, and so forth.

{% hint style="info" %}
**Note**: By default, the response does not include the custom attributes in an API call to a resource ([Categories](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Categories), [Products](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products), [Product Offers](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Product-Offers)). Expanding the `customAttributes=all` query parameter returns all of the configured custom attributes.
{% endhint %}

## Caching responses

To reduce time and consume less bandwidth, you should cache information like the product price on your side. Cached responses improve performance by serving representations directly from the cache rather than the origin server.

You can configure caching in the Commerce API as follows:

* Globally enabled for all cacheable resources
* Enabled per resource
* Set similarly for related resources, such as enabling caching for Offers and Product Offers resources

Only cache responses from GET requests. Caching is not enabled by default. For more information about enabling and configuring caching, contact your Digital River Representative.

## Capturing the customer's IP address

You can capture the customer's IP address using headers. Make sure you account for proxies and forwarded headers when capturing the customer's IP address.

You can capture the customer's IP address using one or more of the following headers:

`$_SERVER['REMOTE_ADDR']`

`$_SERVER['HTTP_X_FORWARDED']`

`$_SERVER['HTTP_CLIENT_IP']`

## Elements

Digital River can add new elements at any time. You should code your implementation to ignore unknown elements and values.
