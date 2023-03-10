---
description: Learn how to change the subscription renewal product.
---

# Changing the subscription renewal product

The following `POST /v1/subscriptions/{subscriptionId}/renewal-product` request changes the subscription renewal product. You must provide the `subscriptionId` and specify the `renewalProductId`. See the [renewal-product](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#renewal-product-resource) resource for more information.

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
