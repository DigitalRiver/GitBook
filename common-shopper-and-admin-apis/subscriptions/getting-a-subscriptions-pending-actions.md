---
description: Learn how to get a subscription's pending actions.
---

# Getting a subscription's pending actions

The following [`GET /v1/subscriptions/{subscriptionId}/pending-actions`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/getSubscriptionPendingActions) returns all actions for a given subscription requested but not processed by the server yet (called pending actions of subscription). You need to provide the `subscriptionId`.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://{host}//v1/subscriptions/{subscriptionId}/pending-actions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
