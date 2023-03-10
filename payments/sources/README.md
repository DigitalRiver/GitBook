---
description: >-
  Learn about the source object and the payment methods supported in the
  Commerce API.
---

# Source basics

A [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)is associated with a [payment method](../../payment-integrations-1/supported-payment-methods.md) that a customer selects to fund a transaction. Digital River retrieves data from the [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)when generating a charge.

In Commerce APIs, each [type of source](./#source-types) has [certain characteristics](./#characteristics-of-payment-methods) that determine how it is created and eventually processed.&#x20;

## Source types

A [source's ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)type represents the [payment method](./#supported-payment-methods) used to create that object.

{% hint style="info" %}
On the [Sources API reference page](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source), you can find a complete list of types and values.
{% endhint %}

A [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)also contains a hash table that corresponds to its `type`. This data object holds detailed information specific to each `type`. For example, a source with a `type` of `credit card` has a `creditCard` hash table that lists the card's `brand`, `expirationMonth`, `expirationYear`, and `lastFourDigits`.

{% tabs %}
{% tab title="First Tab" %}
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

A [source's ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)characteristics revolve around the concepts of [pull or push](./#pull-or-push), [synchronous or asynchronous](./#synchronous-or-asynchronous), [reusable or single-use](./#reusable-or-single-use), [primary or secondary](./#primary-or-secondary), and [payment flow](./#authentication-flow).

### Pull or push

The difference between a pull and push payment [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)has to do with how a customer's funds are transferred.

For pull [sources](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source), customers provide their information and consent, and the money is drawn from their account. No additional customer actions are usually necessary. [Credit cards](../payments-solutions/digitalriver.js/payment-methods/credit-cards.md) are the most common example of this [type of source](./#source-types).

When using a push payment [source](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source), the customer must explicitly send the funds before a charge can become capturable. These payment methods almost always require additional customer action. For example, if you enable [wire transfers](../payments-solutions/digitalriver.js/payment-methods/wire-transfer.md) on your website or app, you'll present your customers with the necessary transfer information to complete the payment and they must "push" the funds.

### Synchronous or asynchronous

With synchronous payment methods, the [`state` ](./#source-state)of the [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)is returned immediately as either `chargeable` or `failed`.  A credit card is an example of this [source type](./#source-types).&#x20;

With asynchronous payment methods, the [source ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)may first return with a `state` of `pending_funds`, `pending_redirect`, or `requires_action` before it can transition to `chargeable`. For example, a source with a type of `payPal` is asynchronous because the customer is redirected to the [PayPal ](../supported-payment-methods/paypal.md)site and must take additional action to authorize the transaction.&#x20;

When integrating asynchronous payment methods, you can [create a webhook](../../events/webhooks/creating-a-webhook.md) to listen for the `source.chargeable` event. This will allow you to determine when you should [attach the source to a cart](./#attaching-a-payment-method-to-an-order-or-cart) or [save the source to a customer's account](./#attaching-a-payment-method-to-a-customer-or-payment-option).

### Reusable or single-use

Some [payment methods](./#supported-payment-methods) can be used to create [sources ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)that are reusable, meaning they support recurring charge authorizations. In customer-initiated transactions, this allows you to present stored sources to customers for convenience purposes. You can also use reusable sources in [subscription ](../../admin-apis/subscription-management/)renewals that are [merchant initiated](../../shopper-apis/cart/submitting-a-cart/initiating-a-charge.md#merchant-initiated).&#x20;

Other [payment methods](./#supported-payment-methods) can only create single-use sources.

{% hint style="success" %}
For a list of payment methods that support reusability, refer to the [Supported payment methods](./#supported-payment-methods) page. Additionally, as part of the enablement process, certain payment methods that are typically reusable can be restricted to single-use only.
{% endhint %}

Sources must have a `reusable` value of `true` before they can be used to make multiple charges.  Reusable sources however can't be created using a [public API key](../../resources/API-structure/#public-keys). So both [Drop-in payments](../payments-solutions/drop-in/) and [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/) only generate single-use sources. To make them reusable once they're created (assuming the source [`type` ](./#source-types)supports re-usability), you must [save the source to a customer](./#attaching-a-payment-method-to-a-customer). This flips `reusable` to `true` and prevents the source's `state` from becoming `consumed` once it's associated with a transaction.

If a source's underlying payment method doesn't support re-usability, we [block the source from being saved to a customer](using-the-source-identifier.md#restrictions-on-saving-sources). So, with a non-reusable source, you should only [attach the source to a cart](./#attaching-a-payment-method-to-an-order-or-cart). This will generate a one-time charge authorization when you convert the cart to an order.&#x20;

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

The Commerce API gives you the ability to save payment sources associated with a customer for later reuse. After you [submit a customer's payment details](../../general-resources/reference/digitalriver-object.md#creating-an-instance-of-drop-in), DigitalRiver.js will create a Source and return a `sourceId`.  You can then use that `sourceId` to [attach the Source to a payment option](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post).

The following examples show how to attach a payment method to a customer or payment option.

{% hint style="warning" %}
You can only attach payment methods that [support recurring payments](../../payment-integrations-1/supported-payment-methods.md). Note that `storeCredit` does not support recurring payments and therefore, you cannot attach it as a payment option.
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
You should only attach a Source whose underlying payment method [supports re-usability](./#reusable-or-single-use). Otherwise, the `reusable` value remains `false` and the customer can't apply that Source to future orders.
{% endhint %}

### Primary or secondary

Refer to [primary and secondary sources](using-the-source-identifier.md#primary-versus-secondary-sources).

### Authentication flow

A [source's ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)`flow` attribute represents how your customers experience the payment process and what actions they must complete. The enumerated values of the attribute are  `standard`, `redirect`, and `receiver`.

* `standard`: In this flow, which mainly applies to [credit cards](../supported-payment-methods/credit-cards.md), you obtain a customer's payment details on your storefront and submit this information to Digital River. The customer is never required to leave your website during the checkout process. No additional action is required by the customer after they submit their information and a charge can be created immediately
* `redirect`: In this flow, you obtain a customer's payment data on your storefront. You then redirect them to the payment provider where they are asked to authorize the transaction. Once the authorization is confirmed, a charge can be created. We recommend you adhere to [these guidelines](../../general-resources/reference/guidelines-for-capturing-payment-details.md#redirect-payment-methods) when using redirect payment methods.&#x20;
* `receiver`: This flow requires that customers push funds to an account before a charge can be created. [Wire transfer](../supported-payment-methods/wire-transfer.md) is a common payment method that uses this authentication flow.&#x20;

## Source state

A source's `state` provides information about what can be done with the object.  The `state` of a source may be `cancelled`, `chargeable`, `consumed`, `failed`, requires\_action, `pending_funds`, or `pending_redirect`.&#x20;

Once charged, the status of [single-use sources](./#reusable-or-single-use) switches to `consumed` and no additional charges can be created from the source. [Reusable sources](./#reusable-or-single-use) however can persist in a `chargeable` state.&#x20;

Sources with a redirect [flow](./#authentication-flow), such as PayPal, often are in a state of `pending_redirect` because the customer must leave your website to confirm the payment.

For sources with a receiver [flow](./#authentication-flow), such as [wire transfers](../supported-payment-methods/wire-transfer.md), it may take days before the funds are confirmed by the receiving bank or financial institution, thereby switching the [source's ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)`state` from `pending_funds` to `chargeable`.

For different success and error scenarios, you can [create tests](../../resources/testing-scenarios.md) to determine whether your integration returns the expected `state` value.

## Source amount

Once all the captures are complete, the customer's payment method is charged the `amount` value contained within the [source](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source), taking into account any cancellations you create or [refunds you issue](../../admin-apis/returns-and-refunds-1/creating-a-satisfaction-refund.md).
