---
description: Learn how to activate a subscription.
---

# Activating a subscription

The following [`POST /v1/subscriptions/{subscriptionId}/activate`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/activateSubscription) request activates a subscription. You need to provide the `subscriptionId` and the `activationKey`.  The `activationDate` and `expirationDate` attributes are optional.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/activate' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
--data-raw '{
  "activationKey" : "{string}",
  "activationDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z"
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response and the subscription state will change from `PendingActivation` to `Subscribed`.
