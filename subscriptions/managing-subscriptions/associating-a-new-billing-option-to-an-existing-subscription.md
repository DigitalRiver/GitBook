---
description: Learn how to associate a new billing option to an existing subscription.
---

# Associating a new billing option to an existing subscription

You can associate a new billing option to an existing subscription by [payment source](associating-a-new-billing-option-to-an-existing-subscription.md#payment-source) or [option](associating-a-new-billing-option-to-an-existing-subscription.md#payment-option).

## Payment source

The following [`POST /v1/subscriptions/{subscriptionId}/payment-source`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentSource) request associates a new billing option to an existing subscription by payment source. You need to provide the `subscriptionId`, and the payment `sourceId`. The `isShippingSameAsBilling` attribute is optional. When set to `true`, the shipping address is the same as the billing address.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/payment-source' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "sourceId": "6260e924-704f-42f2-8f36-b62101d9f904",
  "isShippingSameAsBilling": true
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

When associating a new billing option with an existing subscription by payment source, note the following:

* If the system found a valid billing option by the given `sourceId`, it associates that `sourceId` to the subscription. It does not update any other data for that billing option.
* If it is a valid source and there is no existing billing option associated with this source in Global Commerce, the system creates a new billing option for this given source. Here are the rules in creating a billing option:
  * The system generates a unique nickname for this billing option.
  * If this shopper doesn’t have an existing default billing option, the system sets the default flag to `true` on this new billing option.
  * If this shopper has an existing default billing option, the system sets the default flag to `false` on this new billing option.|

## Payment option

The following [`POST /v1/subscriptions/{subscriptionId}/payment-option`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentOption) request associates a new billing option to an existing subscription by payment option. You need to provide the `subscriptionId`, and the `paymentOptionId`. The `isShippingSameAsBilling` attribute is optional.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://<<host>>/v1/subscriptions/{subscriptionId}/payment-option' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer ***' \
--data-raw '{
 "paymentOptionId": "23443434343434"
 "isShippingSameAsBilling": true
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

