---
description: Learn how to attach a payment method to a cart or customer.
---

# Attaching a payment method to a cart or customer

## Attaching a payment method to an order or cart

The following example shows how to attach a payment method to an order or cart.

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endtab %}
{% endtabs %}

## Attaching a payment method to a customer

The following example shows how to attach a payment option to a customer.

{% tabs %}
{% tab title="POST /v1/shoppers/me/payment-options" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Visa Card",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}
```
{% endtab %}
{% endtabs %}

\
