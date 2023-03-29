---
description: Learn how to change the subscription's external reference identifier.
---

# Changing the subscription's external reference identifier

The following [`POST /v1/subscriptions/{subscriptionId}/reference-id`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/External-Reference/operation/modifyExternalReferenceId) request changes the subscription's external reference identifier. You must provide the `subscriptionId` and specify the `externalReferenceId`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/reference-id' \
--header 'Authorization: Basic  ***' \
...
--data-raw '{
  "externalReferenceId": "123232exteranl"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
