---
description: Learn how to update a subscription's billing and shipping email address.
---

# Updating a subscription's billing and shipping email address

Use the [`POST /v1/subscriptions/{subscriptionId}/email`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Email-Updater/operation/emailUpdater) to update a specific subscription's billing and email address.

{% tabs %}
{% tab title="First Tab" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/email' \
--header 'Authorization: Basic  ***' \
...
--data-raw '{
  "emailAddress": "string"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `200 Accepted` response.
