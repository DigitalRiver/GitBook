---
description: Learn how to resolve problems with API calls.
---

# Troubleshooting API calls

{% hint style="info" %}
**Note**: The examples in this section use `your_access_token` as a placeholder for an actual token.
{% endhint %}

## 401 Error

### Issue

A 401 error occurs when there is a bad Dispatch token or Global Commerce User API token.

### Resolution

Send an API call to identify where the token originated and when it expired. For example:

{% tabs %}
{% tab title="HTTP" %}
```http
GET /oauth20/access-tokens?token=your_access_token  HTTP/1.1
Host: api.digitalriver.com
```
{% endtab %}
{% endtabs %}

The response shows you where the token originated in the domain field and when it expired in the `expiresIn` field.
