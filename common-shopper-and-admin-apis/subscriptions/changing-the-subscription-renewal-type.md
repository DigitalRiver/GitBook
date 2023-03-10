---
description: Learn how to change the subscription renewal type.
---

# Changing the subscription renewal type

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-type`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Subscription-Renewal/operation/updateRenewalType) request changes the subscription renewal type. You need to provide the subscription identifier (`subscriptionId`) and specify the `autoRenewal`. See the [renewal-type](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#renewal-type-resource) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/renewal-type' \
--header 'authorization: bearer ***\
...
--data-raw '{
   "autoRenewal": false
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
