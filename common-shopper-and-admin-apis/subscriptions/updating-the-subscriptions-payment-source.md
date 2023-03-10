---
description: Learn how to update the subscription's payment source.
---

# Updating the subscription's payment source

Use the [`POST /v1/subscriptions/{subscriptionId}/payment-source`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Payment/operation/updatePaymentSource) request to associate a new billing option with an existing subscription by payment option. See the [payment-source](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#payment-source-resouce) resource for more information.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}>/payment-source' \
--header 'authorization: bearer ***\
...
--data-raw '{
    "sourceId": "string",
    "isShippingSameAsBilling": true
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
