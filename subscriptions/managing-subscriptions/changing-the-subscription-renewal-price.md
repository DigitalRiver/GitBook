---
description: Learn how to change the subscription renewal price.
---

# Changing the subscription renewal price

The following [`POST /v1/subscriptions/{subscriptionId}/renewal-price`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/changeSubscriptionRenewalPrice) request changes the subscription renewal price. You need to provide the `subscriptionId` and specify the `renewalUnitPrice`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/renewal-price' \
--header 'Content-Type:  application/json' \
--header 'authorization: Basic ***\
--data-raw '{    
"renewalUnitPrice" : 4
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
