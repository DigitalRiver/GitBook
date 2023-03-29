---
description: Learn how to create session-aware access tokens.
---

# Session-aware access tokens

The session-aware access token links a Global Commerce shopper session to an access token as well as provide the ability to continue a shopper workflow with a previously established shopper session.

To create a session-aware access token, use the `sessionToken` query parameter or `dr_session_token` form parameter, depending on the workflow.

{% hint style="warning" %}
You **must** provide a session-aware token when transitioning a shopper from a 3rd-party application to a Digital River-hosted checkout experience to complete an online purchase.
{% endhint %}

You can create a session-aware token by either sending a browser call or a request to the **Token endpoint** in either the [Shopper API](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers) or the [OAuth API](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Token).

{% hint style="info" %}
If you provide a session token when generating an access token, the system creates a new shopper session.
{% endhint %}

You can choose one of the following options to create a session-aware access token:

* [Creating an anonymous shopper token for a site with an API key](session-aware-access-tokens.md#creating-an-anonymous-shopper-token-for-a-site-with-an-api-key)
* [Creating an anonymous shopper token for a site via OAuth 2.0](session-aware-access-tokens.md#creating-an-anonymous-shopper-token-for-a-site-via-oauth-2.0)

## Creating an anonymous shopper token for a site with an API key

Establish an anonymous shopper (limited access) token in a single call by passing in your API key to the `sessionToken` site action.

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

## Creating an anonymous shopper token for a site via OAuth 2.0

This example requires two calls; one to get the session token, and another to create the access token.

### **Step 1: Get a dr\_session\_token from the `sessionToken` site action with no API key**

{% hint style="warning" %}
You must include the `sessionToken` site action and it **MUST** come from the client side (the shopper's browser). You can do this via ajax, as shown in the following example.
{% endhint %}

{% code title="Example" overflow="wrap" %}
```
function sessionToken() {
       $.ajax({
          url: "https://store.digitalriver.com/store/[siteID]/SessionToken?format=json",
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

### **Step 2: POST the dr\_session\_token to the oauth20 resource, to get an anonymous shopper token.**

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
curl --location -g --request POST 'https://api.digitalriver.com/oauth20/token' \
--header 'Authorization: bearer {{access_token}}' \
...
--data-raw '{
    dr_session_token: [from step #1)
    grant_type: password
    format:json
}'
```
{% endcode %}
{% endtab %}

{% tab title="Response body" %}
{% code overflow="wrap" %}
```json
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
