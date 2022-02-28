---
description: >-
  Learn about the Source object and the payment methods supported in the
  Commerce API.
---

# Sources

The `Source` object represents a customer's payment method.  A [Source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) can be directly [attached to a Cart](broken-reference) to create a one-time charge or saved for future payments by [attaching it to a Customer](broken-reference).&#x20;

Each [payment method](./#payment-methods) supported in the Commerce API has certain features that determine how a Source is created and eventually processed. These features revolve around the concepts of [pull or push](./#pull-or-push), [synchronous or asynchronous](./#synchronous-or-asynchronous), [reusable or single-use](./#reusable-or-single-use), and [authentication flow](./#authentication-flow).

You'll use the DigitalRiver.js library to [create an instance of Drop-in](../../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-an-instance-of-drop-in) and to tokenize the customer's details and payment information.

## Payment methods

A payment method contains the necessary details to create a Source. [Payment integrations](../../payment-integrations-1/) list the [supported payment methods](../../payment-integrations-1/digitalriver.js/payment-methods/) **** and provide instructions on how to create a Source from each method type.&#x20;

Contact your Digital River account manager for details on how to enable different types of payment methods. &#x20;

### Determining the payment method type

The `type` attribute represents the underlying payment method of the Source and is enumerated as a `creditCard`, `directDebit`, `googlePay`, `applePay`,  `payPal`, or `wireTransfer`. When you [retrieve a Source object](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSources), the response contains a hash table with a name that corresponds to the `type` value. For example, a Source with a `type` of `credit card` will contain a hash table called `creditCard`.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "paymentMethod": {
    "type": "creditCard",
    "sourceId": "a231f38d-3a07-4a13-96ed-89693ba7d56c",
    "sourceClientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
    "creditCard": {
      "expirationYear": "2030",
      "lastFourDigits": "0000",
      "clientSecret": "a231f38d-3a07-4a13-96ed-89693ba7d56c_f6d8c951-59c9-4ef3-ac45-9f33c77d2f46",
      "expirationMonth": "08",
      "fundingSource": "debit",
      "brand": "Visa",
    "reusable": "true"
    }
  },
}
```
{% endtab %}
{% endtabs %}

## Characteristics of a payment method

The following sections detail the primary characteristics of how a payment method is charged and how a customer experiences the payment process.

### Pull or push

The difference between a pull and push payment method has to do with how a customer's funds are transferred.

For a pull payment method, customers provide their information and consent, and the money is drawn from their account. No additional customer actions are typically necessary. [Credit cards](../../payment-integrations-1/digitalriver.js/payment-methods/credit-cards.md) are the most common example of this payment method type.

When using a push payment method, the customer must explicitly send the funds before a charge can become capturable. These payment methods almost always require additional customer action. For example, if you enable [wire transfers](../../payment-integrations-1/digitalriver.js/payment-methods/wire-transfer.md) on your website or app, you'll present your customers with the necessary transfer information to complete the payment and they must "push" the funds.

### Synchronous or asynchronous

With synchronous payment methods, the `state` of the Source is returned immediately as either `chargeable` or `failed`.  A credit card is an example of this type of payment method.&#x20;

With asynchronous payment methods, the Source may first return with a `state` of `pending_funds`, `pending_redirect`, or `requires_action` before it can transition to `chargeable`. PayPal is an example of an asynchronous payment method because the customer is redirected to the PayPal site and must take additional action to authorize the transaction.&#x20;

### Reusable or single-use

Some payment methods can be used to create Source objects that are reusable, meaning the customer doesn't need to provide payment details before every transaction.  Other payment methods can only create single-use sources.

With certain exceptions, [payment methods](../../payment-integrations-1/digitalriver.js/payment-methods/) such as Credit Card, GooglePay, Direct Debit, and PayPal are reusable. As part of the enablement process, certain payment methods that are typically reusable can be restricted to single-use. Non-card-based methods however like Wire Transfer, BPay, Konbini, Alipay, Online Banking/IBP, Credit Installment, and Payco are typically single-use only.&#x20;

Sources that can be used to make multiple charges have a `reusable` value of `true`. However, since reusable sources cannot be created using a public API key, the [`createSource`](../../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata) method in [DigitalRiver.js](../../payment-integrations-1/digitalriver.js/) only generates single-use sources. To make them reusable once created (assuming the source type permits re-usability), the Source must be [attached to a payment option](using-the-source-identifier.md#attaching-a-source-to-a-payment-option).

If you don't attach a Source to a Customer, even if the `reusable` value is `true`, then once charged, the `state` of the Source becomes `consumed`.  &#x20;

If the `reusable` value is `false`, then the Source can only be used once. This means that a new Source object must be created every time a customer wants to use this payment method. You should not attach a single-use Source to a Customer if the payment method underlying it does not support re-usability. Rather, you should [assign its identifier](using-the-source-identifier.md#charging-a-single-use-source) to the `sourceId` parameter when issuing a `POST` Checkout request.&#x20;

### Authentication flow

The `flow` attribute represents how your customers experience the payment process and what actions they must take to authenticate a payment method. The enumerated values of the attribute are  `standard`, `redirect`, and `receiver`.

* `standard`: In this flow, which mainly applies to credit cards, you obtain a customer's payment details on your storefront and submit them to Digital River. The customer is never required to leave your website during the checkout process. No additional action is required by the customer after they submit their information and a charge can be created immediately
* `redirect`: With this authentication flow type, you obtain a customer's payment data on your storefront. You then redirect them to the website of the payment method where they are asked to authorize the transaction. Once the authorization is confirmed, a charge can be created. We recommend you adhere to [these guidelines](../../payment-integrations-1/digitalriver.js/reference/guidelines-for-capturing-payment-details.md) when using redirect payment methods.&#x20;
* `receiver`: This flow type requires that a customer push funds to an account before a charge can be created. Bank and wire transfers are two common payment methods that use this authentication flow.&#x20;

## Source state

A payment source also has a `state` attribute, which provides information about what can be done with it.  The `state` of a Source is enumerated by the following values: `cancelled`, `chargeable`, `consumed`, `failed`, and `pending`.&#x20;

Once charged, the status of [single-use sources](./#reusable-or-single-use) switches to `consumed` and no additional charges can be created from the Source. Reusable sources however can maintain a `chargeable` state.&#x20;

Sources that require additional customer action often have a status of `pending` or `cancelled`.  For sources with a redirect, such as PayPal, this is true because the customer must leave your website to confirm the payment. For wire transfers, it may take days before the funds are confirmed by the receiving bank or financial institution and the Source switches to a status of `chargeable`.&#x20;

For different success and error scenarios, you can [create tests](../../payment-integrations-1/testing-scenarios.md) to determine whether your integration returns the expected `state` value.

## Source amount

The customer's payment method is charged the `amount` value of the Source, taking into account any cancellations you create or refunds you issue.

Each time that Digital River returns an updated Source, the value of `amount` can change. For example, if a customer adds or subtracts items from their cart late in the checkout process, and you then submit a new Cart request with the same `sourceId`, the Source is returned with an updated `amount`.
