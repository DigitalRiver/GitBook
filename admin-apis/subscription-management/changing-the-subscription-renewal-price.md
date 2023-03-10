---
description: Learn how to change the subscription renewal price.
---

# Changing the subscription renewal price

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-price`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/changeSubscriptionRenewalPrice) request changes the subscription renewal price. You must provide the `subscriptionId` and specify the `renewalUnitPrice`. See the [Renewal-price](../../general-resources/admin-apis-reference/subscriptions/#renewal-price-source) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/renewal-price' \
--header 'authorization: Basic ***\
...
--data-raw '{    
"renewalUnitPrice" : 4
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
