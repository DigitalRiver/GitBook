---
description: Learn how to create authenticated shopper tokens.
---

# Token



Use the `/oauth20/token` resource to generate either an [anonymous ](tokens.md#creating-an-anonymous-shopper-token)or [authenticated shopper token](tokens.md#creating-authenticated-shopper-tokens). You can also use it to refresh an access token. The API requirements depend on the type of application that invokes a request.

The `/oauth20/token` resource generates an access token that you can use to access resources. A shopper can use an anonymous shopper token to anonymously shop for a product. You need an authenticated shopper token to retrieve authenticated shopper-specific details, such as address or payment details. This token only supports a public workflow.

## Creating a grant OAuth flow for client credentials

Use the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) request to create an authenticated or anonymous shopper token for an application using client credentials (`grant_type={password}`). Include your base64-encoded API key and secret in the request header.&#x20;

{% hint style="danger" %}
Never expose or visibly display the limited or full access tokens created by the APIs to the shopper (such as plain text in a cookie). If a shopper has access to these tokens, there is the potential they could bypass any restrictions built into the store's frontend and place orders directly on our systems via our publicly documented APIs.
{% endhint %}

{% tabs %}
{% tab title="cURL " %}
{% code overflow="wrap" %}
```json
curl --location --request POST 
'https://api.digitalriver.com/oauth20/token?grant_type={password}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "access_token": "your_access_token",
  "token_type": "bearer",
  "expires_in": "3599"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Creating a full-access token using ROPC

To create a full-access token using the ROPC (Resource Owner Password Credentials), use the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post) request and provide the `client_id` and [`grant_type`](oauth-2.0-apis.md#oauth-flows-allowed-by-grant-and-client-types) query parameters.

{% hint style="danger" %}
Never expose or visibly display the limited or full access tokens created by the APIs to the shopper (such as plain text in a cookie). If a shopper has access to these tokens, there is the potential they could bypass any restrictions built into the store's frontend and place orders directly on our systems via our publicly documented APIs.
{% endhint %}

You can only use this [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post)when Digital River maintains the shopper's login and password credentials. If the Digital River partner maintains the shopper's login and password credentials, use the [Client Credentials Grant OAuth flow](broken-reference).

{% tabs %}
{% tab title="cURL " %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/oauth20/token?client_id={clientId}&grant_type={password}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{  
    "access_token": "your_access_token",  
    "token_type": "bearer",  
    "expires_in": "3599",  
    "refresh_token": "your_refresh_token"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Creating an anonymous shopper token

An anonymous shopper token allows a shopper to access the Commerce APIs that do not require a consumer context. This token allows the shopper to send API requests against resources that are not shopper-protected. An anonymous shopper token is an authenticated token. However, it is not an authorized token that provides full access.

You can start an API call by getting an anonymous shopper token. Use the [`POST /oauth/Token?grant_type=password`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(Anonymous%20shopper%20token\)/post) request to get an anonymous shopper token.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'http://api.digitalriver.com/oauth20/token?grant_type=password' \--header 'Authorization: Basic {{authorization}}'
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

To create an anonymous shopper token for a public or confidential application when the shopper wants to shop anonymously, use the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post).

{% hint style="danger" %}
Never expose or visibly display the limited or full access tokens created by the APIs to the shopper (such as plain text in a cookie). If a shopper has access to these tokens, there is the potential they could bypass any restrictions built into the store's frontend and place orders directly on our systems via our publicly documented APIs.
{% endhint %}

## Initiating an authenticated session

Send the following request to create an authenticated shopper token to identify the shopper session:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/oauth20/token' \--header 'Accept: application/json' \--
header 'Content-Type: application/x-www-form-urlencoded' \--header 'Authorization: Basic {{authorization}}'\--
data-urlencode 'dr_external_reference_id={{externalID}}' \--
data-urlencode 'grant_type=client_credentials'
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
```json
{
    "access_token": "your_access_token",
    "token_type": "bearer",
    "expires_in": 3600,
    "refresh_token": "your_refresh_token"
}
```
{% endtab %}
{% endtabs %}

Include your base64-encoded API key and secret in the request header. Include `grant_type=client_credentials` and the `externalReferenceId` in the request body.

This Token API identifies a shopper session and consists of an `access_token` and a `refresh_token`. They correspond to the session cookie and the browser cookie. You can save the `access_token` and `refresh_token` in the application and use them in subsequent queries. The `access_token` expires after a specified interval (60 minutes by default in user session site settings in Digital River. The `refresh_token` expires after one year.

The `expires_in` property is the time-to-live (TTL) value for the access token. You can refresh the access token at any time.

## Getting authenticated shopper tokens

An authenticated shopper token allows the shopper to access all Commerce APIs features. You can only get an authenticated shopper token when the shopper explicitly allows your application to access their data. Only the shopper can grant this token. To get an authorized token, you need to send the shopper to the Digital River platform for authentication. Your application has access to the full API after a shopper enters their credentials and explicitly grants your application permission to access their protected resources. You can use them with your [DigitalRiver.js](../../payments/payments-solutions/digitalriver.js/) JavaScript code.&#x20;

Use the `GET /oauth20/authorize` resource to initiate the creation of an authenticated shopper (full access) token. This resource will return a `302 Found` response that you can use to direct the user to an IDP-hosted login page. After the shopper logs in successfully, control returns to your application through the use of the redirect URI query parameter, which contains a full access token parameter that you can use to make subsequent API calls.

The workflow that an application should implement depends on the type of client, which can be **Public**.

{% hint style="info" %}
You can include an anonymous shopper (limited access) token as a query parameter to transition the shopper state to the authenticated shopper (full access) token.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/oauth20/authorize?client_id={{apikey}}&response_type=token&dr_limited_token={{limited_token}}&redirect_uri={{redirect_uri}}'
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
   "access_token": "your_access_token",
   "token_type": "bearer",
   "expires_in": "3599",

```
{% endcode %}
{% endtab %}
{% endtabs %}
