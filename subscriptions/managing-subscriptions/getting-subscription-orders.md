---
description: Learn how to get subscription orders.
---

# Getting subscription orders

The following [`GET /v1/subscriptions/{subscriptionId}/orders`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getSubscriptionInfo) returns all orders associated with a given subscription. You need to provide the `subscriptionId`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request GET 'http://{host}//v1/subscriptions/{subscriptionId}/orders' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
