---
description: Learn how to change the subscription's external reference identifier.
---

# Changing the subscription's external reference ID

The following [`POST /v1/subscriptions/{subscriptionId}/reference-id`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/modifyExternalReferenceId) request changes the subscription's external reference identifier. You need to provide the `subscriptionId` and specify the `externalReferenceId`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/reference-id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic  ***' \
--data-raw '{
  "externalReferenceId": "123232exteranl"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
