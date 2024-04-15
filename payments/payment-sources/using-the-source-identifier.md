---
description: Learn how to manage payment sources
---

# Managing sources

In th Digital River API, [payment sources](./) fall into two broad categories: [primary and secondary](using-the-source-identifier.md#primary-versus-secondary-sources).

For both categories, after [source creation](using-the-source-identifier.md#creating-payment-sources), you can always [attach a source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) so that Digital River can attempt to generate a [charge](../../order-management/orders/payment-charges/) after you [create the order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). You can also [detach sources from checkouts](using-the-source-identifier.md#detaching-sources-from-checkouts).

If a [primary source](using-the-source-identifier.md#primary-payment-sources) supports [reusability](./#reusable-or-single-use), you may also be able to [save it to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers). For [customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with multiple `sources[]`, we also provide you the ability to [set the default one](using-the-source-identifier.md#setting-the-default-payment-source).

You can [combine primary and secondary sources](using-the-source-identifier.md#combining-primary-and-secondary-payment-sources), but how you sequence their application depends on whether or not the primary source is [reusable](./#reusable-or-single-use).

And when [building your payment flows](../../integration-options/checkouts/building-you-workflows/), the [Digital River object](../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md) exposes methods for [authenticating](using-the-source-identifier.md#authenticating-sources) and [updating](using-the-source-identifier.md#updating-sources) sources that can be useful in purchase and account management scenarios.

## Primary versus secondary sources

When [building your payment workflows](../../integration-options/checkouts/building-you-workflows/), you should be aware of the differences between [primary](using-the-source-identifier.md#primary-payment-sources) and [secondary](using-the-source-identifier.md#secondary-payment-sources) payment sources and how they affect the [payment session](../../integration-options/checkouts/creating-checkouts/payment-sessions.md).

### Primary payment sources

Primary payment [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) are created from traditional [payment methods](../supported-payment-methods/) such as [credit cards](../supported-payment-methods/credit-cards.md), [Google Pay](../supported-payment-methods/google-pay.md), [PayPal](../supported-payment-methods/paypal.md), and [wire transfers](../supported-payment-methods/wire-transfer.md). Most customers use a primary source when making a purchase, but a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sources[]`can only contain one primary source.&#x20;

Primary sources created from [payment methods that support reusability](../supported-payment-methods/) may be able to be [associated with a customer](using-the-source-identifier.md#attaching-sources-to-customers) and then [reused](./#reusable-or-single-use) in future transactions.

Alternatively, you can simply [attach a primary source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts), thereby enabling Digital River to submit a [charge authorization request](../../order-management/orders/payment-charges/#how-a-charge-is-created) after you [create the order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

Once a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) contains a primary source, the [necessary payment preconditions](../../integration-options/checkouts/creating-checkouts/payment-sessions.md#how-to-determine-when-to-create-an-order) are met to [convert that checkout to an order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).&#x20;

### Secondary payment sources

Secondary payment [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) are typically used to supplement a [primary source](using-the-source-identifier.md#primary-payment-sources).&#x20;

In the Digital River APIs, secondary sources have a [`type`](./#supported-payment-methods) of [`customerCredit`](../../integration-options/checkouts/creating-checkouts/applying-a-store-credit.md).

If a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) only contains secondary `sources[]`, you may be able to successfully [create the order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), but before doing so, you need to ensure the [necessary payment preconditions are met](../../integration-options/checkouts/creating-checkouts/payment-sessions.md#how-to-determine-when-to-create-an-order). &#x20;

Secondary sources do not support [reusability](./#reusable-or-single-use). Therefore, they [cannot be saved to a customer's account](using-the-source-identifier.md#restrictions-on-saving-sources). Rather, they can only be [attached to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) to create a one-time [charge](../../order-management/orders/payment-charges/) upon [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation.&#x20;

## Creating payment sources

We provide multiple options for [creating primary sources](using-the-source-identifier.md#creating-primary-sources) and [creating secondary sources](using-the-source-identifier.md#creating-secondary-sources).

### Creating primary sources

[Primary sources](using-the-source-identifier.md#primary-payment-sources) are created with your [public API key](../../administration/dashboard/developers/api-keys/#standard-keys) using [Drop-in payments](../payment-integrations-1/drop-in/drop-in-integration-guide.md) or [DigitalRiver.js with elements](../payment-integrations-1/digitalriver.js/quick-start.md). Once created, you can [attach the source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) or, in some cases, [save the source to a customer](using-the-source-identifier.md#attaching-sources-to-customers).

### Creating secondary sources

How you create [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a [`type`](./#supported-payment-methods) of `customerCredit` depends on the [version](../../general-resources/versioning.md) you're using.

For versions:

* `2021-03-23` and higher, refer to [Applying store credit](../../integration-options/checkouts/creating-checkouts/applying-a-store-credit.md).
* `2020-09-30`, `2020-12-17`, and `2021-02-23`, refer to [Applying store credit (legacy)](../../integration-options/checkouts/creating-checkouts/applying-store-credit-legacy.md).

## Combining primary and secondary payment sources

A [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sources[]` is able to hold a single [primary source](using-the-source-identifier.md#primary-payment-sources) and/or one or more [secondary sources](using-the-source-identifier.md#secondary-payment-sources).

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can combine a secondary source with any primary source that has one of the following [`type`](./#supported-payment-methods) values: `alipayCn`, `creditCard`, `googlePay`, `applePay`, `payPal`, `payPalCredit`, `payPalBilling`, `wireTransfer`, `klarnaCredit`, `klarnaCreditRecurring`, `alipay`, `konbini`, `directDebit` and `onlineBanking`.

You can also use secondary sources with any of the above primary payment sources in [invoices](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices). Just make sure you turn off [billing optimization](../../integration-options/checkouts/subscriptions/invoices.md#invoice-billing). For details, refer to [supported payment methods with invoices](../../integration-options/checkouts/subscriptions/invoices.md#supported-payment-methods).

When [building your workflows](../../integration-options/checkouts/building-you-workflows/), make sure you're properly sequencing the application of primary and secondary sources. The sequence depends on whether you use [secondary sources with a single-use primary source](using-the-source-identifier.md#using-secondary-sources-with-a-single-use-primary-source) or [secondary sources with a saved primary source](using-the-source-identifier.md#using-secondary-sources-with-a-saved-primary-source).

Also, you should be aware of [how Digital River handle captures, cancels, and refunds](using-the-source-identifier.md#how-we-handle-captures-cancels-and-refunds) when an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains multiple [`charges[]`](../../order-management/orders/payment-charges/).

### Using secondary sources with a single use primary source

If a [primary source](using-the-source-identifier.md#primary-payment-sources) is created during the checkout process and then not [associated with a customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers/operation/createCustomerSource) (perhaps because the customer is checking out as a [guest](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#guest-checkouts-or-invoices), the customer is [registered](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) but chooses not to save the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), or the source's [`type`](./#supported-payment-methods) doesn’t support [reusability](./#reusable-or-single-use)), then you must attach all [secondary sources](using-the-source-identifier.md#secondary-payment-sources) to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) before attaching the primary source.

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) primary `sources[]` has a [`reusable`](./#reusable-or-single-use) value that is `false`, then any attempt to [associate a secondary source with the checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) returns the following error:

{% code title="409 Conflict" %}
```
{
    "type": "conflict",
    "errors": [
        {
            "code": "session_update_not_allowed",
            "message": "Updating source is not allowed for the current session state."
        }
    ]
}
```
{% endcode %}

### Using secondary sources with a saved primary source

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) primary [`sources[]`](./) is saved to the [customer making the purchase](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices), then you have more flexibility in how you sequence the application of [primary](using-the-source-identifier.md#primary-payment-sources) and [secondary](using-the-source-identifier.md#secondary-payment-sources) sources.

More specifically, if a checkout's primary `sources[]` has a [`reusable`](./#reusable-or-single-use) value of `true`, then you can request to [associate a secondary source with the checkout](using-the-source-identifier.md#attaching-sources-to-checkouts). Each time this request is successfully submitted, the checkout's primary `sources[].amount` gets reduced by the secondary [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) `amount`.

### How we handle captures, cancels, and refunds

When [combining secondary sources with a primary source](using-the-source-identifier.md#combining-primary-and-secondary-payment-sources), you should be aware of how Digital River processes [captures](using-the-source-identifier.md#captures), [cancels](using-the-source-identifier.md#cancels), and [refunds](using-the-source-identifier.md#refunds) on an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `charges[]`.

#### Captures

Digital River first [captures](../../order-management/orders/payment-charges/#captures) the [charge(s)](../../order-management/orders/payment-charges/) created from [secondary sources](using-the-source-identifier.md#secondary-payment-sources) and then the single charge created from the [primary source](using-the-source-identifier.md#primary-payment-sources).&#x20;

#### Cancels

Digital River first [cancels](../../order-management/orders/payment-charges/#cancels) the single [charge](../../order-management/orders/payment-charges/) created from the [primary source](using-the-source-identifier.md#primary-payment-sources) and then the charge(s) created from [secondary sources](using-the-source-identifier.md#secondary-payment-sources).&#x20;

#### Refunds

Digital River first [refunds](../../order-management/orders/payment-charges/#refunds) the single [charge](../../order-management/orders/payment-charges/) created from the [primary source](using-the-source-identifier.md#primary-payment-sources) and then the charge(s) created from [secondary sources](using-the-source-identifier.md#secondary-payment-sources).&#x20;

## Attaching sources to checkouts

After you [create](using-the-source-identifier.md#creating-payment-sources) or [authenticate](using-the-source-identifier.md#authenticating-sources) a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) and then retrieve its unique identifier, you can use that value to associate the source with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).

You do this by either [sending the source's identifier in the request's payload](using-the-source-identifier.md#sending-a-source-identifier-in-the-request-payload) or [passing its identifier as a path parameter](using-the-source-identifier.md#passing-the-source-identifier-as-a-path-parameter). This is true for both [primary and secondary sources](using-the-source-identifier.md#primary-versus-secondary-sources).

You're only allowed to associate one [primary source](using-the-source-identifier.md#primary-payment-sources) with a checkout. If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sources[]` contains a primary source and you submit a request to attach a different primary source, using either the [payload](using-the-source-identifier.md#sending-a-source-identifier-in-the-request-payload) or [path parameter](using-the-source-identifier.md#passing-the-source-identifier-as-a-path-parameter) approach, then the existing source is replaced.

However, as long as the aggregated `amount` of all of a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sources[]` doesn't exceed the checkout's `totalAmount`, there's no limit to the number of [secondary sources](using-the-source-identifier.md#secondary-payment-sources) you can attach to a checkout.&#x20;

### Passing a source's identifier in the request body <a href="#sending-a-source-identifier-in-the-request-payload" id="sending-a-source-identifier-in-the-request-payload"></a>

To associate a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can send its `sourceId` in the body of a [`POST /checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts) or [`POST /checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) request.

```
curl --location --request POST 'https://api.digitalriver.com/checkouts/177642590336' \
--header 'Authorization: <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
   "sourceId": "7a3ce24c-5e18-4b8d-a667-d64a513ed33f"
}'
```

### Passing a source's identifier as a path parameter <a href="#passing-the-source-identifier-as-a-path-parameter" id="passing-the-source-identifier-as-a-path-parameter"></a>

To associate a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can pass the checkout's identifier and the source's identifier as path parameters in a [`POST /checkouts/{id}/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/attachSourceToCheckout).&#x20;

## Detaching sources from checkouts

When you need to remove a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) from a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can send a [`DELETE  /checkouts/{id}/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/detachSourceToCheckout). A successful request returns a `204 No Content` status code and an empty body. &#x20;

If the source's [`reusable`](./#reusable-or-single-use) value is `false` when you submit the detach request, then the source's [`state`](./#source-state) transitions to `cancelled`, and any attempt to [reattach the source to a checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) returns the following error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "source_status_invalid_for_session",
            "message": "The source status is invalid for this session."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Saving sources to customers <a href="#attaching-sources-to-customers" id="attaching-sources-to-customers"></a>

In some cases, after you [create a primary payment source](using-the-source-identifier.md#creating-primary-sources), you can save it to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) for use in future [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).&#x20;

Attaching [sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) to [customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can be useful when [building workflows](../../integration-options/checkouts/building-you-workflows/) that allow customers to save their payment information during [one-off purchases](../../integration-options/checkouts/building-you-workflows/#credit-card-details-saved-by-customer-during-checkout), [subscription acquisitions](../../integration-options/checkouts/building-you-workflows/#customer-enters-credit-card-details-during-subscription-acquisition-checkout), or on [account management pages](../../integration-options/checkouts/building-you-workflows/#saving-a-credit-card-for-future-use).

As long as the [necessary preconditions](using-the-source-identifier.md#restrictions-on-saving-sources) are satisfied, you can save a [primary source](using-the-source-identifier.md#primary-payment-sources) to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) by sending their unique identifiers as path parameters in a [`POST/customers/{customerId}/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCustomerSource) request.

```
curl --location --request POST 'https://api.digitalriver.com/customers/544671250336/sources/05642ad9-d227-4250-a73e-92514ef68620' \
...
--data-raw ''
```

A successful request flips the source's [`reusable`](./#reusable-or-single-use) value to `true` and returns the source.&#x20;

{% tabs %}
{% tab title="200 OK" %}
```javascript
{
    "id": "05642ad9-d227-4250-a73e-92514ef68620",
    "createdTime": "2021-09-16T14:29:45Z",
    "type": "creditCard",
    "reusable": true,
    "state": "chargeable",
    "customerId": "544671250336",
    "owner": {
        ...
    },
    "clientSecret": "05642ad9-d227-4250-a73e-92514ef68620_be853d8e-0422-436e-af3e-45f8a92b25e9",
    "creditCard": {
        "brand": "Visa",
        "expirationMonth": 7,
        "expirationYear": 2027,
        "lastFourDigits": "1111"
    },
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

At this point, you can update your system and notify customers that the payment method has been saved to their account.

### Restrictions on saving sources

Prior to sending a [save source to customer request](using-the-source-identifier.md#attaching-sources-to-customers), make sure that the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) doesn't have any [reusability](using-the-source-identifier.md#reusability-restrictions) and [chargeability](using-the-source-identifier.md#chargeability-restrictions) restrictions.

#### Reusability restrictions

If a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) doesn't support [reusability](./#reusable-or-single-use) and you pass its identifier in a [`POST/customers/{customerId}/sources/{sourceId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCustomerSource), then the following error is returned:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "nonreusable_source",
            "message": "Only a reusable source may be attached to a customer."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
For a list of payment methods that can be used in recurring transactions, refer to the [Supported payment methods](../supported-payment-methods/) page.&#x20;

With [Drop-in payments](../payment-integrations-1/drop-in/), you can also use `supportsStorage` in the [`onSuccess`](../payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event's `data` to make this determination.&#x20;
{% endhint %}

#### Chargeability restrictions

Only [source's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) whose [`state`](./#source-state) is `chargeable` can successfully be saved to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers). If the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) isn't `chargeable` (perhaps because it has a `redirect` payment [`flow`](./#authentication-flow), the customer has yet to successfully authorize payment, and, as a result, its [`state`](./#source-state) is still `pending_redirect`), and you attempt to [save the source to a customer](using-the-source-identifier.md#attaching-sources-to-customers), you'll receive the following error:

{% code title="409 Conflict" %}
```
{
    "type": "conflict",
    "errors": [
        {
            "code": "source_not_chargeable",
            "parameter": "sourceId",
            "message": "Source 'ea6b3297-d05f-4d5d-a12d-95234e93d450' is not chargeable."
        }
    ]
}
```
{% endcode %}

{% hint style="info" %}
With [Drop-in payments](../payment-integrations-1/drop-in/), you can use `readyForStorage` in the [`onSuccess`](../payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event's `data` to determine whether a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) can be associated with a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).&#x20;
{% endhint %}

### Restrictions on using saved sources

A [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) saved to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can't be used to [generate a charge](../../order-management/orders/payment-charges/#how-a-charge-is-created) unless you associate the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).&#x20;

If a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) has a saved `sources[]`, and you [associate that source with the checkout](using-the-source-identifier.md#attaching-sources-to-checkouts) but neglect to [associate that customer with the checkout](../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices), you'll receive the following error when you [convert the checkout to an order](../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "source_in_use",
            "parameter": "sourceId",
            "message": "Source '37dcb9dc-c1ea-4295-b787-7d872e94cefd' is attached to a different customer."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Removing sources from customers <a href="#detaching-sources-from-customers" id="detaching-sources-from-customers"></a>

If you'd like to detach a payment [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) saved to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers), you can send a [`DELETE/customers/{id}/sources/{sourcesId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteCustomerSource) request. When you do so, the source's [`state`](./#source-state) becomes `cancelled` and the resource can't be used to [create any future charges](../../order-management/orders/payment-charges/#how-a-charge-is-created).

If you attempt to reattach this source to a customer, you'll receive the following error:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "source_not_chargeable",
            "parameter": "sourceId",
            "message": "Source '24f4f281-9613-4d6d-8831-808952ed4915' is not chargeable."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Setting the default payment source

[Customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can store multiple payment `sources[]`.

The first [source you attach to a customer](using-the-source-identifier.md#attaching-sources-to-customers) automatically becomes its default, and its identifier is assigned to the customer's `defaultSourceId` attribute. If you'd like to assign a customer a different default payment source, you must first ensure it's [attached to the customer](using-the-source-identifier.md#attaching-sources-to-customers). Once that's done, you can set its identifier as the `defaultSourceId` in an [update customer request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCustomers).

## Authenticating sources

After you [retrieve a source](retrieving-sources.md), you can pass its identifier, [payment session](../../integration-options/checkouts/creating-checkouts/payment-sessions.md) identifier, and client secret to the [authenticate source method](../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#authenticating-sources) in the [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started) library. This operation is especially helpful when [building workflows](../../integration-options/checkouts/building-you-workflows/) that allow customers to retrieve saved credit card information during [one-off purchases](../../integration-options/checkouts/building-you-workflows/#customer-selects-saved-credit-card-during-checkout) or [subscription acquisitions](../../integration-options/checkouts/building-you-workflows/#customer-saves-credit-card-details-during-subscription-acquisition-checkout).

## Updating sources

After you [retrieve a source](retrieving-sources.md), you can pass its identifier, [payment session](../../integration-options/checkouts/creating-checkouts/payment-sessions.md) identifier, and client secret to the [update source method](../payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#updating-sources) in the [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started) library. This operation is useful when [building workflows](../../integration-options/checkouts/building-you-workflows/) that allow customers to [update a credit card's expiration date or billing address](../../integration-options/checkouts/building-you-workflows/#updating-a-credit-cards-expiration-date-or-billing-address).
