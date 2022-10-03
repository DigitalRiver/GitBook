---
description: Understand the Global Commerce Access token.
---

# Global Commerce access token

There are two ways to access the Product Admin: you using a [secret key](../../../resources/API-structure.md#private-keys) or a Global Commerce access token. There is no difference between the secret key and the Global access token. Ask your Digital River representative to enable the Global Commerce access token if you want to use this feature.

The Global Commerce access token allows you to directly access Global Commerce. You must provide your Global Commerce user credentials to get the access token (`access_token`). You can use the access token value provided in the response as your `Bearer` token in your product requests to access the Product Admin API.

{% hint style="success" %}
We recommend using the [secret key](../../../resources/API-structure.md#private-keys) because the access token will expire in one day by default. The `expires_in` value determines when the access token will expire. You will have to request a new access token when the current access token expires.
{% endhint %}

<mark style="background-color:orange;">??? Is this the correct request for a client? Or is this example for internal DR users? If it's not the correct request for a client, please provide the correct request. ???</mark>

{% tabs %}
{% tab title="HTTP access request" %}
{% code overflow="wrap" %}
```http
POST /auth HTTP/1.1
Host: dispatch-test.digitalriver.com
Content-Type: application/x-www-form-urlencoded
Authorization: Basic dispatchKey:dispatchSecret encoded by BASE64
 
username=your_DRCC_loginId&grant_type=password&password=your_DRCC_passwordEncodedByBASE64
```
{% endcode %}
{% endtab %}

{% tab title="JSON access response" %}
{% code overflow="wrap" %}
```json
{
    "access_token": "the-token-value",
    "token_type": "bearer",
    "expires_in": 300
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
