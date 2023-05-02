---
description: Learn the basics of sources.
---

# Source basics

A [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is associated with a [payment method](../supported-payment-methods/) that a customer selects to fund a transaction. Digital River retrieves data from the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) when generating a charge.

In Commerce APIs, each source type has certain characteristics that determine how it is created and eventually processed.&#x20;

## Supported payment methods

You can use various payment methods in Commerce API to create a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources). For a complete list, refer to the [Supported payment methods](./#supported-payment-methods) page.&#x20;

A source's `type` represents the payment method used to create that object. You can find a complete list of these `type` values on the [Sources API reference](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Email-Updater/operation/emailUpdater) page.&#x20;

A source also contains a hash table with a name that corresponds to its `type`. This data object holds detailed information specific to that `type`. For example, a source with a `type` of `credit card` has a `creditCard` hash table that lists the card's `brand`, `expirationMonth`, `expirationYear`, and `lastFourDigits`.

{% tabs %}
{% tab title="Source" %}
{% code overflow="wrap" %}
```json
{
    ...
    "type": "creditCard",
    ...
    "creditCard": {
        "brand": "MasterCard",
        "expirationMonth": 5,
        "expirationYear": 2025,
        "lastFourDigits": "0008"
    },
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Characteristics of payment methods

The following sections detail the primary characteristics of how a payment method is charged and how a customer experiences the payment process.

### Pull or push

The difference between a pull and push payment method involves how a customer's funds are transferred.

Customers provide their information and consent for a pull payment method, and the money is drawn from their account. No additional customer actions are typically necessary. [Credit cards](../payments-solutions/digitalriver.js/payment-methods/credit-cards.md) are the most common example of this payment method type.

When using a push payment method, the customer must explicitly send the funds before a charge can become capturable. These payment methods almost always require additional customer action. For example, suppose you enable [wire transfers](../payments-solutions/digitalriver.js/payment-methods/wire-transfer.md) on your website or app. In that case, you'll present your customers with the necessary transfer information to complete the payment and reusable sources, and they must "push" the funds.

### Synchronous or asynchronous

With synchronous payment methods, the [`state` ](./#source-state)of the source is returned immediately as either `chargeable` or `failed`. A credit card is an example of this type of payment method.&#x20;

With asynchronous payment methods, the source may first return with a `state` of `pending_funds`, `source_pending_redirect`, or `requires_action` before it can transition to `chargeable`. PayPal is an example of an asynchronous payment method because the customer is redirected to the PayPal site and must take additional action to authorize the transaction.&#x20;

### Reusable or single-use

You can use some [payment methods](./#supported-payment-methods) to create reusable sources (recurring payments). This means the customer doesn't need to re-supply the payment details before every transaction. Other [payment methods](./#supported-payment-methods) can only create single-use sources.

{% hint style="success" %}
Refer to the S[upported payment methods](./#supported-payment-methods) page for a list of payment methods that support reusability. Additionally, as part of the enablement process, certain payment methods that are typically reusable can be restricted to single-use only.
{% endhint %}

Sources must have a `reusable` value of `true` before they can be used to make multiple charges. Reusable sources can't be created using a [public API key](../../resources/API-structure/#public-keys). So both [Drop-in payments](../payments-solutions/drop-in/) and [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/) only generate single-use sources. To make them reusable once they're created (assuming the source `type` supports reusability), you must [save the source to a customer](./#attaching-a-payment-method-to-a-customer). This flips `reusable` to `true` and prevents the source's `state` from becoming `consumed` once it's associated with a transaction.

If a source's underlying payment method doesn't support reusability, we [block the source from being saved to a customer](using-the-source-identifier.md#restrictions-on-saving-sources). So, with a non-reusable source, you should only [attach the source to a cart](./#attaching-a-payment-method-to-an-order-or-cart). When you convert the cart to an order, this will generate a one-time charge authorization.&#x20;

#### Attaching a payment method to an order or cart

The following example shows how to attach a payment method to an order or cart.

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```json
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Attaching a payment method to a customer or payment option

The Commerce API allows you to save payment sources associated with a customer for later reuse. After you [submit a customer's payment details](../../general-resources/reference/digitalriver-object.md#creating-an-instance-of-drop-in), DigitalRiver.js will create a Source and return a `sourceId`.   You can then use that `sourceId` to [attach the Source to a payment option](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post).

The following examples show how to attach a payment method to a customer or payment option.

{% hint style="warning" %}
You can only attach payment methods that [support recurring payments](../supported-payment-methods/). Note that `storeCredit` does not support recurring payments, so you cannot attach it as a payment option.
{% endhint %}

{% tabs %}
{% tab title="Attaching source to a customer" %}
<pre class="language-json" data-overflow="wrap"><code class="lang-json"><strong>curl --location --request POST 'https://&#x3C;&#x3C;host>>/v1/shoppers/me/payment-options' \
</strong><strong>--header 'Content-Type:  application/json' \
</strong>--header 'authorization: bearer ***\
--data-raw '
{
  "paymentOption": {
    "nickName": "My Visa Card",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}                                                                                                                                                            
</code></pre>
{% endtab %}

{% tab title="Attaching a source to a payment option" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://<<host>>/v1/shoppers/me/payment-options' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '
{
  "paymentOption": {
    "nickName": "My Token",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
You should only attach a Source whose underlying payment method [supports reusability](./#reusable-or-single-use). Otherwise, the `reusable` value remains `false`, and the customer can't apply that Source to future orders.
{% endhint %}

### Primary or secondary

Refer to [primary and secondary sources](using-the-source-identifier.md#primary-versus-secondary-sources).

### Payment method's authentication flow

A source's `flow` attribute represents how your customers experience the payment process and what actions they must take to authenticate a [payment method](./#supported-payment-methods). The enumerated values of the attribute are  `standard`, `redirect`, and `receiver`.

* `standard`: In this flow, which mainly applies to credit cards, you obtain a customer's payment details on your storefront and submit this information to Digital River. The customer is never required to leave your website during the checkout process. The customer requires no additional action after they submit their information, and a charge can be created immediately
* `redirect`: This authentication flow type lets you obtain a customer's payment data on your storefront. You then redirect them to the payment method website, asking them to authorize the transaction. Once the authorization is confirmed, a charge can be created. We recommend you adhere to [these guidelines](https://docs.digitalriver.com/digital-river-api/payments/payment-integrations-1/digitalriver.js/reference/guidelines-for-capturing-payment-details#redirect-payment-methods) when using redirect payment methods.&#x20;
* `receiver`: This flow type requires that a customer push funds to an account before a charge can be created. Bank and wire transfers are two common payment methods that use this authentication flow.&#x20;

## Source state

A payment source also has a `state` attribute which provides information about what can be done with it. The following values enumerate the `state` of a Source: `cancelled`, `chargeable`, `consumed`, `failed`, and `pending`.&#x20;

Once charged, the status of [single-use sources](./#reusable-or-single-use) switches to `consumed`, and no additional charges can be created from the Source. [Reusable sources](./#reusable-or-single-use), however, can maintain a `chargeable` state.&#x20;

Sources with a redirect [authentication payment flow](./#payment-flow), such as PayPal, often are in a state of `pending_redirect` because the customer must leave your website to confirm the payment.

For sources with a receiver [authentication payment flow](./#payment-flow), such as wire transfers, it may take days before the funds are confirmed by the receiving bank or financial institution, thereby switching the source from `pending_funds` to `chargeable`.

For different success and error scenarios, you can [create tests](../../resources/testing-scenarios.md) to determine whether your integration returns the expected `state` value.

## Source amount

Once all the captures are complete, the customer's payment method is charged the `amount` value contained within the source, considering any cancellations you create or refunds you issue.
