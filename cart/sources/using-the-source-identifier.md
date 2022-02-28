---
description: >-
  Learn how a Source identifier can be used to charge a single-use Source,
  attach a Source to a Customer, or select a different default payment method.
---

# Using the source identifier

The `sourceId` attribute in the Apply Payment Method resource and the Payment Options resource uniquely identify a [Source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) object. The following sections describe common scenarios in which you might use these identifier values.&#x20;

## Charging a single-use source

Your storefront may be configured so that customers are not required to create an account or sign-in to make a purchase. In this case, after you submit the guest customer's payment details, [DigitalRiver.js](../../payment-integrations-1/digitalriver.js/) will [create a Source](https://app.gitbook.com/@digital-river/s/digital-river-api/\~/drafts/-MDaNXfT3-egaY-AJaqe/getting-started-1/basic-process-flow#creating-a-source-and-order) and return the `sourceId` .  You can then use a [POST /apply-payment-method](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Payment-Method/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to set the `sourceId` attribute.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://<<host>>/v1/shoppers/me/carts/active/apply-payment-method' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}'
```
{% endtab %}
{% endtabs %}

Since the Source is not attached to a Shopper, this payment method object [cannot be re-used](./#reusable-or-single-use) for future purchases, and once used, its state becomes `consumed`.

## Attaching a source to a payment option

The Commerce API gives you the ability to save payment sources associated with a customer for later reuse. After you [submit a customer's payment details](../../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in), DigitalRiver.js will create a Source and return a `sourceId`.  You can then use that `sourceId` to [attach the Source to a payment option](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post).

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://<<host>>/v1/shoppers/me/payment-options' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "paymentOption": {
    "nickName": "My Token",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}'
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
You should only attach a Source whose underlying payment method [supports re-usability](./#reusable-or-single-use). Otherwise, the `reusable` value remains `false` and the customer can't apply that Source to future orders.
{% endhint %}

## Switching the default payment source

Registered customers may have multiple saved payment methods associated with their account. These Source objects are stored in the `sources` array of the [Payment Options](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options) resource.&#x20;

The first Source attached to a Customer becomes the default payment method where `isDefault` is set to `true` and its identifier is assigned to the `sourceId` attribute. If you'd like to assign a different payment method as the default, simply submit a [`POST /payment-options/{id}`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) request where `{id}` is the new default payment method and set `isDefault` to `true`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://<<host>>/v1/shoppers/me/payment-options/{id}' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "paymentOption" : {
    "nickName" : "Credit Card",
    "isDefault" : "true",
    "sourceId":"{{sourceId}}"
  }
}'
```
{% endtab %}
{% endtabs %}
