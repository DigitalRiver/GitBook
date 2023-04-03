---
description: Learn how to change the subscription renewal product.
---

# Changing the subscription renewal product

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-product`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/updateRenewalProduct) request changes the subscription renewal product. You must provide the `subscriptionId` and specify the `renewalProductId`.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/renewal-product' \
--header 'Authorization: Basic ***' \
...
--data-raw '{
  "renewalProductId" :"5329012900"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

This request allows you to upgrade or downgrade the renewal product.
