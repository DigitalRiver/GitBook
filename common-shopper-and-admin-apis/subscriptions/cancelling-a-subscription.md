---
description: Learn how to cancel a subscription by the subscription identifier.
---

# Cancelling a subscription

The following [`POST /v1/subscriptions/{subscriptionId}/cancel`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Manage-Subscription/operation/cancelSubscription) request cancels the subscription by the subscription identifier. You must provide the subscription identifier (`subscriptionId`) and set the suppress cancel notification (`suppressCancelNotification`) to `true`. See the [Cancel ](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#cancel-resource)resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/cancel' \
--header 'authorization: bearer ***\
...
--data-raw '{
 "suppressCancelNotification": true
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

****
