---
description: Learn how to change the subscription renewal date (expiration date).
---

# Updating the subscription renewal date

The following [`POST /v1/subscriptions/{subscriptionId}/expiration-date`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Subscription/operation/updateExpirationDate) request changes the quantity of the renewed subscription. You must provide the `subscriptionId` and specify the `expirationDate`. The expiration date must be the current or future date. See the [expiration date](../../general-resources/admin-apis-reference/subscriptions/#expiration-date-resource) resource for a description of the attributes.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/expiration-date' \
--header 'Authorization: Basic ****' \
...
--data-raw '{
  "expirationDate":"2020-10-19T01:23:48.000-0500"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
