---
description: Learn how to change the subscription renewal date (expiration date).
---

# Changing the subscription renewal date

The following [`POST /v1/subscriptions/{subscriptionId}/expiration-date`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updateExpirationDate) request changes the quantity of the renewed subscription. You need to provide the `subscriptionId` and specify the `expirationDate`. The expiration date must be the current or future date.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/expiration-date' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ****' \
--data-raw '{
  "expirationDate":"2020-10-19T01:23:48.000-0500"
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
