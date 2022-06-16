---
description: Learn how to change the quantity of the renewed subscription.
---

# Changing the subscription renewal quantity

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-quantity`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/changeSubscriptionRenewalQuantity) request changes the quantity of the renewed subscription. You need to provide the `subscriptionId` and specify the `renewalQuantity`. In the following example, the value for the `renewalQuantity` is `2`.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/renewal-quantity' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer ***' \
--data-raw '{
"renewalQuantity": 2
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
