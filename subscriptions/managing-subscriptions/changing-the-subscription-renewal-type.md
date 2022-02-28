---
description: Learn how to change the subscription renewal type.
---

# Changing the subscription renewal type

The following [`POST /v1/subscriptoins/{subscriptionId}/renewal-type`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updateRenewalType) request changes the subscription renewal type. You need to provide the `subscriptionId` and specify the `autoRenewal`.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://{host}/v1/subscriptions/{subscriptionId}/renewal-type' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
   "autoRenewal": false
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
