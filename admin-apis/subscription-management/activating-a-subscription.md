---
description: Learn how to activate a subscription.
---

# Activating a subscription

The following [`POST /v1/subscriptions/{subscriptionId}/activate`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Subscription/operation/activateSubscription) request activates a subscription. You must provide the `subscriptionId` and the `activationKey`.  The `activationDate` and `expirationDate` attributes are optional. The expiration date must be the current or future date. See the [activate](../../general-resources/admin-apis-reference/subscriptions/#activate-resource) resource for a description of the attributes.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/activate' \
--header 'Authorization: Basic ***' \
...
--data-raw '{
  "activationKey" : "{string}",
  "activationDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response and the subscription state will change from `PendingActivation` to `Subscribed`.
