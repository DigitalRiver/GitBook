---
description: Learn how to reduce the quantity of a subscription.
---

# Reducing the quantity of a subscription

In this scenario, the customer has two subscriptions and decided to reduce the subscription product to one.&#x20;

Use the [`POST /v1/subscriptions/{subscriptionId}/reduce`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Immediate-Midterm-Change/operation/reduceSubscription) resource to reduce the quantity of a subscription. You need to include the product identifier (`id`) and the updated quantity (`quantity`). In the following example, the value for the `quantity` is `1`.  See the [reduce ](broken-reference)resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}>/reduce' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "product" : {
    "id" : "5410723500"
  },
  "quantity" : 1
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 OK response" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}>/reduce' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "product" : {
    "id" : "5410723500"
  },
  "quantity" : 1
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}
