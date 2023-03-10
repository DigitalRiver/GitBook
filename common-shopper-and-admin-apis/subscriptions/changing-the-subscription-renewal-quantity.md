---
description: Learn how to change the quantity of the renewed subscription.
---

# Changing the subscription renewal quantity

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-quantity`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/changeSubscriptionRenewalQuantity) request changes the quantity of the renewed subscription. You need to provide the subscription identifier (`subscriptionId`) and specify the renewal quantity (`renewalQuantity`). In the following example, the value for the `renewalQuantity` is `2`. See the [renewal-quantity](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#renewal-quantity-resource) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/renewal-quantity' \
--header 'Authorization: Bearer ***' \
...
--data-raw '{
"renewalQuantity": 2
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
