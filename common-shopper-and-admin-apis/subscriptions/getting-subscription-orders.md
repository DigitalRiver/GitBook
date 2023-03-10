---
description: Learn how to get subscription orders.
---

# Getting subscription orders

The following [`GET /v1/subscriptions/{subscriptionId}/orders`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Retrieve-Subscription/operation/getSubscriptionInfo) returns all orders associated with a given subscription. You need to provide the subscription identifier (`subscriptionId`).&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://{host}//v1/subscriptions/{subscriptionId}/orders' \
--header 'Authorization: Basic ***' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
