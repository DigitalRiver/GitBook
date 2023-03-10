---
description: Learn how to manage sources.
---

# Managing sources

## Best practice flows by payment type



<mark style="background-color:orange;">??? Where do</mark> [<mark style="background-color:orange;">Wire Transfer</mark>](../supported-payment-methods/wire-transfer.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">PayPal Pay in 4</mark>](../supported-payment-methods/paypal-pay-in-4.md)<mark style="background-color:orange;">, and</mark> [<mark style="background-color:orange;">PayPal Pay in 3</mark>](../supported-payment-methods/paypal-pay-in-3.md) <mark style="background-color:orange;">fit in? ???</mark>

### Standard and delayed payment flow

Use the following flow for standard payments such as [Apple Pay](../supported-payment-methods/apple-pay.md), [credit cards](../supported-payment-methods/credit-cards.md), [Google Pay](../supported-payment-methods/google-pay.md), [iDEAL](../supported-payment-methods/ideal.md), and delayed payments such as <mark style="background-color:orange;">xxx</mark>. <mark style="background-color:orange;">??? For delayed payments, do you mean</mark> [<mark style="background-color:orange;">Alipay</mark>](../supported-payment-methods/alipay.md)<mark style="background-color:orange;">?  ???</mark>

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post). <mark style="background-color:orange;">??? I'm assuming you mean a billing address. Is that correct? ???</mark>
3. [Create a source with a session identifier (`paymentSessionId`)](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/createSources). The source `state` is `chargeable`.
4. [Attach the source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Redirect then submit payment flow

Use the following flow for standard payments such as [PayPal ](../supported-payment-methods/paypal.md)and [Klarna](../supported-payment-methods/klarna.md). <mark style="background-color:orange;">??? Does this apply to</mark> [<mark style="background-color:orange;">Afterpay</mark>](../supported-payment-methods/afterpay.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">Alipay</mark>](../supported-payment-methods/alipay.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">Bancontact</mark>](../supported-payment-methods/bancontact.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">BLIK</mark>](../supported-payment-methods/blik.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">FPX Online Banking</mark>](../supported-payment-methods/fpx-online-banking.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">iDEAL</mark>](../supported-payment-methods/ideal.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">Online Banking (IBP)</mark>](../supported-payment-methods/online-banking-ibp.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">Online Banking (Korea Bank Transfer)</mark>](../supported-payment-methods/online-banking-ibp.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">PayCo</mark>](../supported-payment-methods/payco.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">PayPal Billing Agreement</mark>](../supported-payment-methods/paypal-billing-agreement.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">PayPal Credit</mark>](../supported-payment-methods/paypal-credit.md)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">PayPal RatenZahlung (Installment Payment)</mark>](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-ratenzahlung)<mark style="background-color:orange;">,</mark> [<mark style="background-color:orange;">SEPA Direct Debit</mark>](../supported-payment-methods/sepa-direct-debit.md)<mark style="background-color:orange;">, and</mark> [<mark style="background-color:orange;">TreviPay</mark>](../supported-payment-methods/trevipay.md)<mark style="background-color:orange;">, too? What about KlarnaCredit Recurring? ???</mark>

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post). <mark style="background-color:orange;">??? I'm assuming you mean a billing address. Is that correct? ???</mark>
3. [Create a source with a session identifier (`paymentSessionId`)](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/createSources). The source `state` is `requires_confirmation`.
4. [Attach the source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart). The session `state` is `requires_confirmation`.
5. Complete the redirect authorization.
6. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Submit then redirect payment flow

Use the following flow for [Trustly](../supported-payment-methods/trustly.md).

1. [Create the shopper token](../../shopper-apis/shopper-basics/common-use-cases/creating-a-customer.md).
2. [Apply shopper and their billing address to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post). <mark style="background-color:orange;">??? I'm assuming you mean a billing address. Is that correct? ???</mark>
3. [Create a source with a session identifier (`paymentSessionId`)](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/createSources). The source state is `pending_redirect`.
4. [Attach the source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart). The session `state` is `requires_confirmation`.
5. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/). The session `state` is `pending_redirect`.
6. Complete redirect authorization. The session `state` is `chargeable`.
7. [Resume cart](../../shopper-apis/cart/resuming-cart-submission.md) to complete post-order processing.

### Submit a Boleto payment flow

To use Boleto as a payment method:

1. [Create a cart](../../shopper-apis/cart/creating-or-updating-a-cart/#creating-a-cart).
2. Optional. Set the locale and currency.\
   `curl --location --request GET 'https://{host}/v1/shoppers/me.json?locale=pt_BR&currency=BRL' \`\
   `--header 'Content-Type: application/json'`\
   `--header 'authorization: bearer ***\`
3. Optional. Set the cart address to the BR address.
4. [Attach the tax ID to the cart](../../shopper-apis/cart/managing-tax-identifiers.md#attaching-a-tax-identifier-to-a-cart). This action inserts the tax ID into the payment session.
5. [Create a Boleto source with a payment session ID](using-the-source-identifier.md#step-2-create-a-boleto-source-using-digitalriver.js). Note that the tax ID is required when creating the Boleto source. The payment session ID provides the tax ID.
6. [Apply the source to the cart](./#attaching-a-payment-method-to-a-customer-or-payment-option).
7. [Submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Return, refund, or cancel through Global Commerce

<mark style="background-color:orange;">??? Need more information. ???</mark>

## Primary versus secondary sources

In the Commerce API, there are two broad categories of payment sources: [primary and secondary](using-the-source-identifier.md#primary-versus-secondary-sources).

For both categories, after you [create a payment source](using-the-source-identifier.md#creating-payment-sources), you can always [attach it to a cart](./#attaching-a-payment-method-to-an-order-or-cart) so that we can use it to generate a one-time charge. You can also [detach sources from carts](using-the-source-identifier.md#detaching-payment-sources-from-a-cart).

If a [primary source](using-the-source-identifier.md#primary-payment-sources) supports [reusability](./#reusable-or-single-use), you may be able [save it to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers). For [shoppers ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers)with multiple saved payment `sources[]`, we also provide you the ability to [set the default one](using-the-source-identifier.md#setting-the-default-payment-source).

You can [combine primary and secondary sources](using-the-source-identifier.md#combining-primary-and-secondary-payment-sources), but how you sequence their application depends on whether or not the primary source is [reusable](./#reusable-or-single-use).

And when [building your payment flows](../building-your-workflows.md), the [DigitalRiver object](../../general-resources/reference/digitalriver-object.md) exposes methods for [authenticating ](using-the-source-identifier.md#authenticating-sources)and [updating](using-the-source-identifier.md#updating-sources) sources that can be useful in purchase and account management scenarios.

When [building your payment workflows](../building-your-workflows.md), you should be aware of the differences between [primary ](using-the-source-identifier.md#primary-payment-sources)and [secondary ](using-the-source-identifier.md#secondary-payment-sources)payment sources and how they affect the [payment session](../../shopper-apis/cart/payment-sessions.md).

### Primary payment sources

Primary payment [sources ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)are created from traditional [payment methods](../../payment-integrations-1/supported-payment-methods.md) such as [credit cards](../supported-payment-methods/credit-cards.md), [Google Pay](../supported-payment-methods/google-pay.md), [PayPal](../supported-payment-methods/paypal.md), and [wire transfers](../supported-payment-methods/wire-transfer.md). Most customers use a primary source when making a purchase, but a [cart ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper)can only contain one.&#x20;

Primary sources created from [payment methods that support reusability](../../payment-integrations-1/supported-payment-methods.md) may be able to be [associated with a customer](./#attaching-a-payment-method-to-a-customer-or-payment-option) and then [reused ](./#reusable-or-single-use)in future transactions.

Alternatively, you can simply [attach a primary source to a cart](./#attaching-a-payment-method-to-an-order-or-cart), thereby enabling Digital River to submit a charge authorization request after you [submit the cart](../../shopper-apis/cart/submitting-a-cart/).

### Secondary payment sources

Secondary payment [sources ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source)are typically used to supplement a [primary source](using-the-source-identifier.md#primary-payment-sources).

{% hint style="info" %}
For the Commerce API, [`customerCredit` ](../../shopper-apis/shopper-basics/common-use-cases/applying-store-credit.md)is currently the only type of supported secondary source.     &#x20;
{% endhint %}

You can successfully submit an order entirely with secondary sources, but you need to ensure the [payment session state](../../shopper-apis/cart/payment-sessions.md#session-state) is valid and the [amount contributed is sufficient](../../shopper-apis/cart/payment-sessions.md#session-state).

You cannot edit the `amount` value for a secondary source. To change the `amount` value for the secondary source:

1. [Detach the primary source](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/delete) (or simply [detach all sources from the cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1payment/delete)).
2. [Create a new secondary source](using-the-source-identifier.md#creating-secondary-sources) with the correct amount.
3. [Attach the new secondary source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).
4. If needed, [attach the primary source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).

{% hint style="info" %}
Always attach the secondary source to the cart first. The primary source will cover the remaining amount. If you attach the primary source first, the primary source will cover the entire amount and the secondary source will be ignored when the order is submitted.
{% endhint %}

Secondary sources do not support [reusability](./#reusable-or-single-use). Therefore, they [cannot be saved to a customer's account](using-the-source-identifier.md#restrictions-on-saving-sources). They should only be [attached to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) to create a one-time charge when that cart is submitted.

## Creating payment sources

We provide multiple options for [creating primary sources](using-the-source-identifier.md#creating-primary-sources) and [creating secondary sources](using-the-source-identifier.md#creating-secondary-sources).

### Creating primary sources

You can create [primary sources](using-the-source-identifier.md#primary-payment-sources) with your [public API key](../../resources/API-structure/#public-keys) using [Drop-in Payments](../payments-solutions/drop-in/) or [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/). Once the [source is `chargeable`](./#source-state), you should either [attach the source to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) or [save the source to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers).

### &#x20;Creating secondary sources

You create [secondary sources](using-the-source-identifier.md#secondary-payment-sources) through the [Sources API ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources)by sending your [confidential API key](../../resources/API-structure/api-keys.md#confidential-keys) in a `POST/sources` request.

When defining the request, you retrieve the [payment session identifier](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts#payment-session-identifier) from the cart you're building. The `amount` is optional, except when the `type` is `customerCredit`. The `type` is required and we currently only support `customerCredit`. You must also send an empty hash table whose name matches the `type`.

The `owner` hash table is optional and can be used to meet our billing address requirements. You can provide the owner information, including the address when creating a secondary source.&#x20;

{% hint style="info" %}
We recommend that you do not provide an [owner object](../payments-solutions/digitalriver.js/payment-methods/common-payment-objects.md#owner-object) with the secondary source. This ensures that the wrong address is not applied to the cart which will trigger a payment auth failed error.
{% endhint %}

The `upstreamId` parameter is useful for mapping the source to your credit management system.

{% tabs %}
{% tab title="POST/sources request" %}
{% code overflow="wrap" %}
```
curl --location --request POST 'https://api.digitalriver.com/sources' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "paymentSessionId": "ps_8cecaa32-f692-44cc-b103-4cf24dc93913",
    "amount": 2,
    "type": "customerCredit",
    "customerCredit": {}
    "upstreamId": "7765374748",
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

A `201 OK` response returns a unique [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) in a [`chargeable` state](./#source-state). You should [attach it to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) so that we can use it to generate a one-time charge.

{% tabs %}
{% tab title="POST/sources response" %}
{% code overflow="wrap" %}
```javascript
{
    "id": "99fe8ad1-999e-4e13-95d5-248e472aa7c8",
    "createdTime": "2021-02-24T21:59:05Z",
    "type": "customerCredit",
    "currency": "USD",
    "amount": 2.0,
    "reusable": false,
    "state": "chargeable",
    "clientSecret": "99fe8ad1-999e-4e13-95d5-248e472aa7c8_a8c8bbb4-e9da-4cd7-a3c3-3a00272ced18",
    "customerCredit": {},
    "paymentSessionId": "ps_8cecaa32-f692-44cc-b103-4cf24dc93913",
    "upstreamId": "7765374748",
    "liveMode": false
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Combining primary and secondary payment sources

You can associate a [primary payment source](using-the-source-identifier.md#primary-payment-sources) with only one [secondary payment source](using-the-source-identifier.md#secondary-payment-sources).

In the Cart API, the following payment methods support the use of `customerCredit`: [Credit Cards](../payments-solutions/digitalriver.js/payment-methods/credit-cards.md),  [Google Pay](../payments-solutions/digitalriver.js/payment-methods/google-pay.md), [Klarna](../payments-solutions/digitalriver.js/payment-methods/klarna.md), [PayPal Express Checkout](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-express-checkout-digital-wallet), [PayPal Credit](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-credit), [PayPal Billing Agreement](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-billing-agreement), and [Wire Transfer](../payments-solutions/digitalriver.js/payment-methods/wire-transfer.md).

{% hint style="info" %}
We currently only support `customerCredit` as a secondary source.
{% endhint %}

### Attaching multiple payment sources to the cart

You can only associate one primary source with a cart. If there's a primary source in the cart and you try to attach a different primary source, [remove all attached sources](using-the-source-identifier.md#detaching-sources-from-a-cart) or [remove the attached primary payment source](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Payment-Method/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) directly from the cart, then attach new sources to the cart.&#x20;

{% hint style="danger" %}
When using multiple sources in a cart, always apply the secondary sources first. Apply the primary source last.
{% endhint %}

For a list of payment methods that support reusability, refer to the [Supported payment methods](../../payment-integrations-1/supported-payment-methods.md).  &#x20;

To attach two sources to a cart, choose one of the following best practices.

#### Best practice 1: Use /apply-payment-method

Use the following steps for both authenticated shoppers and anonymous shoppers.

1. Send the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a secondary source.
2. Send the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a primary source.

#### Best practice 2: Use /apply-payment-method and /apply-shopper

Use the following steps only for authenticated shoppers.

1. Send the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a secondary source
2. Send the  [`POST /apply-shopper`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post) request to attach the primary source. The default payment option saved to the shopper will be applied to the cart when applying a shopper. Note that the shopper can only save the primary source to their account.

### Address information

When you attach a source to the cart using the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) and the cart already has address information, the system will not use the `source` address. It will use the existing address in the cart. If the cart does not have the address information, the system will copy the address from the `source` to the cart.&#x20;

This behavior applies to both primary and secondary sources. This is why we recommend that you don't include the owner's information when you [create a secondary source](using-the-source-identifier.md#creating-secondary-sources).

When you attach a source to a shopper using [`POST /payment-options`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post), the system will save the source's payment information and address to the shopper's payment options, and associate the address with the payment. When you apply a shopper to a cart using [`POST /apply-shopper`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post), the system will apply the shopper's default payment method and copy the address associated with the payment method to the card, regardless of whether the cart has an address available or not.

### Amount contributed from each payment source

After applying the payment source to the cart, the amount contributed by the payment source appears in the `amountContributed` field for the `paymentMethod` object in the /cart, /submit-cart, and /order responses.

{% code title="Single payment example" overflow="wrap" %}
```json
{
    "paymentMethod": {
        "type": "creditCard",
        "sourceId": "ba462e2a-885e-4436-9c9a-e8a3988daa49",
        "sourceClientSecret": "ba462e2a-885e-4436-9c9a-e8a3988daa49_bd6910cf-1bae-413e-b4d0-98034efe527c",
        "creditCard": {
            "expirationYear": "2525",
            "lastFourDigits": "1111",
            "clientSecret": "ba462e2a-885e-4436-9c9a-e8a3988daa49_bd6910cf-1bae-413e-b4d0-98034efe527c",
            "expirationMonth": "8",
            "brand": "Visa",
            "flow": "standard",
            "reusable": "false"
        },
        "amountContributed": {
            "currency": "USD",
            "value": 68.01
        }
    }
}
```
{% endcode %}

{% code title="Two payment methods example" overflow="wrap" %}
```json
        "paymentMethod": {
            "type": "creditCard",
            "sourceId": "d86502e8-5252-48e2-bd82-c2fe6de8810b",
            "sourceClientSecret": "d86502e8-5252-48e2-bd82-c2fe6de8810b_66601535-e527-489a-9b5c-847e9e940aed",
            "creditCard": {
                "expirationYear": "2525",
                "lastFourDigits": "1111",
                "clientSecret": "d86502e8-5252-48e2-bd82-c2fe6de8810b_66601535-e527-489a-9b5c-847e9e940aed",
                "expirationMonth": "8",
                "brand": "Visa",
                "flow": "standard",
                "reusable": "false"
            },
            "amountContributed": {
                "currency": "USD",
                "value": 68.01
            },
            "supplementaryPaymentMethods": [
                {
                    "type": "customerCredit",
                    "sourceId": "4db130f3-2302-43f2-9f7a-eed3835e1a7e",
                    "sourceClientSecret": "4db130f3-2302-43f2-9f7a-eed3835e1a7e_6b7e2d5a-9037-46a8-8632-4d90b0113ffa",
                    "customerCredit": {
                        "clientSecret": "4db130f3-2302-43f2-9f7a-eed3835e1a7e_6b7e2d5a-9037-46a8-8632-4d90b0113ffa",
                        "flow": "standard",
                        "reusable": "false"
                    },
                    "amountContributed": {
                        "currency": "USD",
                        "value": 50
                    }
                }
            ]
        },
```
{% endcode %}

### Amount contribution of the entire order

The `paymentSession` object shows the following information for an entire order:

* `amountContributed`: indicates the accumulated contributed amount of the attached payment sources.
* `amountRemainingToBeContributed`: indicates the gap amount required to fulfill the order. If the value is not zero that means the shopper should apply an additional payment to the cart to cover the order's total amount.

{% code title="paymentSession example" overflow="wrap" %}
```json
{
    "paymentSession": {
        "id": "3c9bf484-2ec5-46f8-8e88-5f126f026187",
        "clientSecret": "3c9bf484-2ec5-46f8-8e88-5f126f026187_668c5e4d-0a80-4338-9dce-3825f0831782",
        "status": "requires_confirmation",
        "amountContributed": {
            "currency": "USD",
            "value": 118.01
        },
        "amountRemainingToBeContributed": {
            "currency": "USD",
            "value": 0
        }
    }
}
```
{% endcode %}

### Detaching payment sources from a cart

Use one of the following options to remove all attached sources directly from a cart.

* ``[`DELETE v1/shoppers/me/carts/active/apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/delete) removes a payment source from the cart. Use this option and include the source ID in the payload to remove payment sources one by one.
* ``[`DELETE v1/shoppers/me/carts/active/payment`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1payment/delete) removes all attached sources directly from the cart

When finished, you can [attach new sources](using-the-source-identifier.md#attaching-multiple-sources-to-the-cart) to the cart.

### Refunds

If a customer requests a refund, the system will refund the [primary payment source](using-the-source-identifier.md#primary-payment-sources) first. Once the system fully refunds the primary source, the system will use the [secondary payment source](using-the-source-identifier.md#secondary-payment-sources) to refund the remaining value.&#x20;

For example, a customer purchased a line item quantity of 10 for a total of $1000. They used $600 from their primary payment source (for example, a credit card) and $400 from their secondary payment source (for example, store credit) to pay for the order. If the customer requests a refund of $400, the system refunds $400 to their credit card. If the customer requests a refund of $700, the system refunds $600 to their credit card and $100 to their store credit.

## Charging a single-use payment source

Your storefront may be configured so that customers are not required to create an account or sign in to make a purchase. In this case, after you submit the guest customer's payment details, [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/) will [create a Source](../../general-resources/reference/digitalriver-object.md#createsource-sourcedata) and return the `sourceId` .  You can then use a [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to set the `sourceId` attribute.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://<<host>>/v1/shoppers/me/carts/active/apply-payment-method' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

Since the Source is not attached to a Shopper, this payment method object [cannot be reused](./#reusable-or-single-use) for future purchases, and once used, its state becomes `consumed`.

## Switching the default payment source

Registered customers may have multiple saved payment methods associated with their accounts. These Source objects are stored in the `sources` array of the [Payment Options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options) resource.&#x20;

The first Source attached to a Customer becomes the default payment method where `isDefault` is set to `true` and its identifier is assigned to the `sourceId` attribute. If you'd like to assign a different payment method as the default, simply submit a [`POST /payment-options/{id}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) request where `{id}` is the new default payment method and set `isDefault` to `true`.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://<<host>>/v1/shoppers/me/payment-options/{id}' \
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
{% endcode %}
{% endtab %}
{% endtabs %}
