---
description: Learn how to update the subscription's payment option.
---

# Updating the subscription's payment option.

Use the [`POST /v1/subscriptions/{subscriptionId}/payment-option`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Payment/operation/updatePaymentOption) request to associate a new billing option with an existing subscription by payment option. See the [payment-option](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#payment-option-resource) resource for more information.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}>/payment-option' \
--header 'authorization: bearer ***\
...
--data-raw '{
    "paymentOptionId": "string",
    "isShippingSameAsBilling": true    
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
