---
description: Learn the basics of sources.
---

# Source basics

A [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is associated with the customer's [payment method](../supported-payment-methods/) that a customer uses to fund a transaction. When [generating a charge](../../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created), Digital River retrieves data from the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources).

In the Digital River APIs, each [source type](./#supported-payment-methods) has [certain characteristics](./#characteristics-of-payment-methods) that determine how it's created and how a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) is eventually processed.&#x20;

## Source types <a href="#supported-payment-methods" id="supported-payment-methods"></a>

A [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `type` represents the [payment method](../supported-payment-methods/) used to create that object.&#x20;

{% hint style="info" %}
On the [Sources API reference page](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), you can find a complete list of `type` values.
{% endhint %}

A [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) also contains a hash table that corresponds to its `type`. This data object holds detailed information specific to each `type`. For example, a source with a `type` of `credit card` has a `creditCard` hash table that lists the card's `brand`, `expirationMonth`, `expirationYear`, and `lastFourDigits`.

{% tabs %}
{% tab title="Source " %}
```javascript
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
{% endtab %}
{% endtabs %}

## Characteristics of payment sources <a href="#characteristics-of-payment-methods" id="characteristics-of-payment-methods"></a>

A [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) characteristics revolve around the [pull or push](./#pull-or-push), [synchronous or asynchronous](./#synchronous-or-asynchronous), [reusable or single-use](./#reusable-or-single-use), [primary or secondary](./#primary-or-secondary), and [payment flow](./#authentication-flow).

### Pull or push

The difference between a pull and push payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) involves how a customer's funds are transferred.

With pull [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), customers provide their information and consent, and the money is drawn from their accounts. No additional customer actions are usually necessary. Credit cards are the most common example.

When using a push payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), the customer must explicitly send the funds before a [charge can become capturable](../../developer-resources/digital-river-api-reference/payment-charges.md). These payment sources almost always require additional customer action. For example, if you enable [wire transfers](../supported-payment-methods/wire-transfer.md) on your website or app, you'll need to [present your customers with the necessary transfer information](../../order-management/creating-and-updating-an-order.md#handling-pending-payment-orders) to complete payment, and they must then "push" the funds.

### Synchronous or asynchronous

With synchronous payment methods, the [`state`](./#source-state) of the resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is returned immediately as either `chargeable` or `failed`. A credit card is an example of this source [`type`](./#supported-payment-methods).

With asynchronous payment methods, the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) may first return in `state` of `pending_funds`, `pending_redirect`, or `requires_action` before it transitions to `chargeable`. For example, a source with a [`type`](./#supported-payment-methods) of `payPal` is asynchronous because the customer is redirected to the [PayPal](../supported-payment-methods/paypal.md) site and must take additional action to authorize the transaction.

When integrating asynchronous payment methods, you can [create a webhook](../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of `source.chargeable`. This will allow you to determine when to [attach the source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) or [save the source to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers).

### Reusable or single-use

Some [payment methods](../supported-payment-methods/) can be used to create reusable [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), meaning they support recurring [charge authorizations](../../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created). In customer-initiated transactions, you can present [stored sources](using-the-source-identifier.md#attaching-sources-to-customers) to customers for convenience. You can also use reusable sources in [merchant-initiated](../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#merchant-initiated) [subscription](../../integration-options/checkouts/subscriptions/) renewals.

Other [payment methods](../supported-payment-methods/) only create single-use [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources).

{% hint style="success" %}
Refer to the [Supported payment methods](../supported-payment-methods/) page for a list of payment methods that support recurring payments. Additionally, as part of the enablement process, certain payment methods that are typically reusable can be restricted to single-use only.
{% endhint %}

[Sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) must have a `reusable` value of `true` before they can be used to make multiple [charges](../../developer-resources/digital-river-api-reference/payment-charges.md). Reusable sources can't be created using a [public API key](../../administration/dashboard/developers/api-keys/#standard-keys). As a result, both [Drop-in payments](../payment-integrations-1/drop-in/drop-in-integration-guide.md) and [DigitalRiver.js with elements](../payment-integrations-1/digitalriver.js/quick-start.md) only generate single-use sources. To make them reusable once created (assuming the source's [`type`](./#supported-payment-methods) supports reusability), you must [save the source to a customer](using-the-source-identifier.md#attaching-sources-to-customers). This flips `reusable` to `true` and prevents the source's [`state`](./#source-state) from becoming `consumed` once it's associated with the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

If a source's underlying payment method doesn't support reusability, we [block the source from being saved to a customer](using-the-source-identifier.md#restrictions-on-saving-sources). As a result, with non-reusable sources, you should only [attach the source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts). When you [convert the checkout to an order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), this will generate a one-time [charge authorization](../../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created).

### Primary or secondary

Refer to [primary and secondary sources](using-the-source-identifier.md#primary-versus-secondary-sources)

### Authentication flow <a href="#authentication-flow" id="authentication-flow"></a>

A [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `flow` represents how your customers experience the payment process and what authentications they must complete. The enumerated `flow` values are `standard`, `redirect`, and `receiver`.

* `standard`: In this flow, which mainly applies to [credit cards](../supported-payment-methods/credit-cards.md), you obtain a customer's payment details on your storefront and submit this information to Digital River. The customer is never required to leave your website during the checkout process. Customers require no additional action after they submit their information, and a [charge](../../developer-resources/digital-river-api-reference/payment-charges.md) can be created immediately
* `redirect`: In this flow, you obtain a customer's payment data on your storefront. You then redirect them to the payment provider, asking them to authorize the transaction. Once the authorization is confirmed, a [charge](../../developer-resources/digital-river-api-reference/payment-charges.md) can be created. We recommend you adhere to [these guidelines](../../developer-resources/reference/guidelines-for-capturing-payment-details.md#redirect-payment-methods) when using redirect payment methods.
* `receiver`: This flow requires that customers push funds to an account before a [charge](../../developer-resources/digital-river-api-reference/payment-charges.md) can be created. [Wire transfer](../supported-payment-methods/wire-transfer.md) is a common payment method that uses this authentication flow.

## Source state

A [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `state` provides information about what can be done with the object. The source's `state` may be `cancelled`, `chargeable`, `consumed`, `failed`, `requires_action`, `pending_funds`, or `pending_redirect`.

Digital River only [creates a charge object](../../developer-resources/digital-river-api-reference/payment-charges.md#how-a-charge-is-created) when the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is `chargeable`. You can listen for `source.chargeable` [events](../../order-management/events-and-webhooks-1/events-1/) to be notified of when the source transitions to this `state`.

Once charged, the `state` status of [single-use sources](./#reusable-or-single-use) switches to `consumed` , and no additional charges can be created from the Source. [Reusable sources](./#reusable-or-single-use), however, can maintain a `chargeable` state.&#x20;

Sources with a [`flow`](./#authentication-flow) of `redirect`, such as [PayPal](../supported-payment-methods/paypal.md), often are in a `state` of `pending_redirect` because the customer must leave your website to confirm the payment.

For sources with a [`flow`](./#authentication-flow) of `receiver`, such as [wire transfers](../supported-payment-methods/wire-transfer.md), it may take days before the funds are confirmed by the receiving bank or financial institution, thereby switching the [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `state` from `pending_funds` to `chargeable`.

For different success and error scenarios, you can [create tests](../../developer-resources/testing-scenarios.md) to determine whether your integration returns the expected `state`.

## Source amount

Once all [captures are complete](../../developer-resources/digital-river-api-reference/payment-charges.md#captures), the customer's payment method is charged the `amount` value contained within the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), considering any [cancellations you create](../../order-management/informing-digital-river-of-a-fulfillment.md) or [refunds you issue](../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md).

Each time that Digital River returns an updated [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), the value of `amount` can change. For example, if customers add or subtract items from their carts late in the checkout process, and you then [update the checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts), the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is returned with an updated `amount`.
