---
description: Learn how to cancel a subscription by the subscription identifiers.
---

# Cancelling a subscription

The following [`POST /v1/subscriptions/{subscriptionId}/cancel`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/cancelSubscription) request cancels the subscription by the subscription identifier. You need to provide the `subscriptionId` and set `suppressCancelNotification` to `true`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://{host}>/v1/subscriptions/{subscriptionId}/cancel' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
 "suppressCancelNotification": true
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

