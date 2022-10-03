---
description: Learn how to reduce the quantity of a subscription with add-ons.
---

# Reducing the quantity of a subscription

In this scenario, the customer wants to reduce the quantity of their subscription with add-ons.

Use the [`POST /v1/subscriptons/{subscriptionId}/reduce`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/reduceSubscription) resource to reduce the quantity of a customer's subscription. You need to include the product identifier (`id`) and the updated quantity (`quantity`). In the following example, the value for the `quantity` is `1`. You'll receive a `202 Accepted` response.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/reduce' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "product" : {
    "id" : "5367865200"
  },
  "quantity" : 1,
  "addOns" : [ {
    "product" : {
      "id" : "5400082600"
    },
    "quantity" : 1
  }, {
    "product" : {
      "id" : "5400082700"
    },
    "quantity" : 1
  } ]
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
