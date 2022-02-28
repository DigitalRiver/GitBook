---
description: Learn how to change the subscription renewal product.
---

# Changing the subscription renewal product

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-product`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updateRenewalProduct) request changes the subscription renewal product. You need to provide the `subscriptionId` and specify the `renewalProductId`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://{host}/v1/subscriptions/{subscriptionId}/renewal-product' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
--data-raw '{
  "renewalProductId" :"5329012900"
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

This request allows you to upgrade or downgrade the renewal product.
