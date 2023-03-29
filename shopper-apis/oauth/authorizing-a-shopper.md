---
description: Learn how to authorize a shopper.
---

# Authorizing a shopper

The workflow that an application should implement depends on the type of client, which can be Public.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request GET 'https://api.digitalriver.com/oauth20/authorize?redirect_uri=http%253A%252F%252Fexample.com&client_id=a78b756bd47e258841d7f007f3f62a&response_type=token&dr_limited_token=6c6bfd0fb07be35c608a2b8e5f5ae72e' \
...'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The response body should be empty.
{% endtab %}
{% endtabs %}
