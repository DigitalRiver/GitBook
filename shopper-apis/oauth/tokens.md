---
description: Learn how to create authenticated shopper tokens.
---

# Token

Use the `/oauth20/token` resource with client credentials (`grant_type=password`) to generate either an [anonymous ](tokens.md#creating-an-anonymous-shopper-token)or [authenticated shopper token](tokens.md#initiating-an-authenticated-session-returning-shopper-or-login-shopper). The API requirements depend on the type of application that invokes a request. A shopper can use an anonymous shopper token to anonymously shop for a product. You need an authenticated shopper token to retrieve authenticated shopper-specific details, such as address or payment details. This token only supports a public workflow.

The `/oauth20/token` resource generates an access token that you can use to access resources. You can also use it to refresh an access token.&#x20;

{% hint style="danger" %}
Never expose or visibly display the limited or full access tokens created by the APIs to the shopper (such as plain text in a cookie). If a shopper has access to these tokens, there is the potential they could bypass any restrictions built into the store's frontend and place orders directly on our systems via our publicly documented APIs.
{% endhint %}

## Creating an anonymous shopper session (guest checkout)

An anonymous shopper token allows a shopper to access the Commerce APIs that do not require a consumer context. This token allows the shopper to send API requests against resources that are not shopper-protected. An anonymous shopper token is an authenticated token. However, it is not an authorized token that provides full access.

To create an anonymous shopper token for a public or confidential application when the shopper wants to shop anonymously, use the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(ROPC\)/post). When you create an anonymous shopper token for an application using client credentials, include your base64-encoded API key and secret in the request header.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 
'https://api.digitalriver.com/oauth20/token?grant_type=password' \
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

## Initiating an authenticated session (returning shopper or login shopper)

An authenticated shopper token allows the shopper to access all Commerce APIs features. You can only get an authenticated shopper token when the shopper explicitly allows your application to access their data. Only the shopper can grant this token. To get an authorized token, you need to send the shopper to the Digital River platform for authentication. Your application has access to the full API after a shopper enters their credentials and explicitly grants your application permission to access their protected resources.&#x20;

### Option 1

Before a returning shopper signs in, send the [`POST /oauth20/token?grant_type=password`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(Anonymous%20shopper%20token\)/post) request.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```html
curl --location --request POST 
'https://api.digitalriver.com/oauth20/token?grant_type=password' \
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

When the shopper signs in, send the [`POST /oauth20/token`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token/paths/\~1oauth20\~1token%20\(Client%20credentials\)/post) request to create an authenticated shopper token for the shopper session. When you create an authenticated shopper token for an application using client credentials, include your base64-encoded API key and secret in the request header.&#x20;

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

### Option 2

Before the returning shopper signs in, use the `GET /oauth20/authorize` resource to initiate the creation of an authenticated shopper (full access) token. This resource will return a `302 Found` response that you can use to direct the user to an IDP-hosted login page. After the shopper logs in successfully, control returns to your application through the use of the redirect URI query parameter, which contains a full access token parameter that you can use to make subsequent API calls.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/oauth20/authorize?client_id={apikey}&response_type=token&dr_limited_token={limited_token}&redirect_uri={redirect_uri}'
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

The workflow that an application should implement depends on the type of client, which can be **Public**.

{% hint style="info" %}
You can include an anonymous shopper (limited access) token as a query parameter to transition the shopper state to the authenticated shopper (full access) token.
{% endhint %}

This Token API identifies a shopper session and consists of an `access_token` and a `refresh_token`. They correspond to the session cookie and the browser cookie. You can save the `access_token` and `refresh_token` in the application and use them in subsequent queries. The `access_token` expires after a specified interval (60 minutes by default in user session site settings in Digital River. The `refresh_token` expires after one year.

The `expires_in` property is the time-to-live (TTL) value for the access token. You can refresh the access token at any time.
