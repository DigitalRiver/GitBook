---
description: Learn how to manage sources.
---

# Managing sources

In the Commerce API, there are two broad categories of payment sources: [primary and secondary](using-the-source-identifier.md#primary-versus-secondary-sources).

For both categories, after you [create a payment source](using-the-source-identifier.md#creating-payment-sources), you can always [attach it to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) so that we can use it to generate a one-time charge. You can also [detach sources](using-the-source-identifier.md#detaching-sources-from-cart) from carts.

Once you [create a primary source](using-the-source-identifier.md#creating-primary-sources) that supports [reusability](./#reusable-or-single-use), you can [save it to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers). For customers who have multiple saved payment sources, we also provide you the ability to [set the default one](using-the-source-identifier.md#setting-the-default-payment-source).

You can [combine primary and secondary sources](using-the-source-identifier.md#combining-primary-and-secondary-payment-sources).

And when building your payment flows, the DigitalRiver.js library contains methods for [authenticating ](using-the-source-identifier.md#authenticating-sources)and [updating](using-the-source-identifier.md#updating-sources) sources that can be useful in purchase and account management scenarios.

## Primary versus secondary sources

When building your payment workflows, you should be aware of the differences between [primary ](using-the-source-identifier.md#primary-payment-sources)and [secondary ](using-the-source-identifier.md#secondary-payment-sources)payment sources and how they affect the [payment session](../../cart/payment-sessions.md).

### Primary payment sources

Primary payment sources are created from [traditional payment methods](../payments-solutions/digitalriver.js/payment-methods/) such as credit cards, Google Pay, PayPal, and wire transfers. Nearly all transactions are conducted with a primary source, but each order can only contain one. Once you [create them](using-the-source-identifier.md#creating-primary-sources) and then [attach them to a customer](using-the-source-identifier.md#attaching-sources-to-customers), primary sources can be re-used in future transactions (assuming the underlying payment method supports [reusability](./#reusable-or-single-use)). You can also [attach them to a cart](using-the-source-identifier.md#attaching-sources-to-customers) so we can use them to create a one-time charge.

Each time that Digital River returns an updated Source, the value of `amount` can change. For example, if a customer adds or subtracts items from their cart late in the checkout process, and you then submit a new Cart request with the same `sourceId`, the Source is returned with an updated `amount`.

Once they are successfully associated with a transaction, primary sources move the [payment session into the necessary state](../../cart/payment-sessions.md#session-state) and fully fund the transaction.

### Secondary payment sources

Secondary payment sources are typically used to supplement a [primary source](using-the-source-identifier.md#primary-payment-sources) such as [store credit](../../consumer-browsing-experience-1/common-use-cases/applying-store-credit.md).

{% hint style="info" %}
For the Commerce API, [`customerCredit` ](../../consumer-browsing-experience-1/common-use-cases/applying-store-credit.md)is currently the only type of supported secondary source.     &#x20;
{% endhint %}

You can successfully submit an order entirely with secondary sources, but you need to ensure the [payment session state](../../cart/payment-sessions.md#session-state) is valid and the [amount contributed is sufficient](../../cart/payment-sessions.md#session-state).

You cannot edit the `amount` value for a secondary source. To change the `amount` value for the secondary source:

1. [Detach the primary source](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/delete) (or simply [detach all sources from the cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1payment/delete)).
2. [Create a new secondary source](using-the-source-identifier.md#creating-secondary-sources) with the correct amount.
3. [Attach the new secondary source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).
4. If needed, [attach the primary source to the cart](using-the-source-identifier.md#attaching-multiple-payment-sources-to-the-cart).

{% hint style="info" %}
Always attach the secondary source to the cart first. The primary source will cover the remaining amount. If you attach the primary source first, the primary source will cover the entire amount and the secondary source will be ignored when the order is submitted.
{% endhint %}

Secondary sources do not support [reusability](./#reusable-or-single-use). Therefore, they [cannot be saved to a customer's account](using-the-source-identifier.md#restrictions-on-saving-sources). They should only be [attached to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) to create a one-time charge when that cart is converted to an order.

## Creating payment sources

We provide multiple options for [creating primary sources](using-the-source-identifier.md#creating-primary-sources) and [creating secondary sources](using-the-source-identifier.md#creating-secondary-sources).

#### Creating primary sources

You create [primary sources](using-the-source-identifier.md#primary-payment-sources) with your [public API key](../../resources/API-structure.md#public-keys) using [Drop-in Payments](../payments-solutions/drop-in/) or [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/). Once the [source is `chargeable`](./#source-state), you should either [attach the source to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) or [save the source to a customer's account](using-the-source-identifier.md#attaching-sources-to-customers).

#### Creating secondary sources

You create [secondary sources](using-the-source-identifier.md#secondary-payment-sources) through the [Sources API ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources)by sending your [private API key](../../resources/API-structure.md#private-keys) in a `POST/sources` request.

When defining the request, you retrieve the [payment session identifier](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts#payment-session-identifier) from the cart you're building. The `amount` is optional, except when the `type` is `customerCredit`. The `type` is required and we currently only support `customerCredit`. You must also send an empty hash table whose name matches the `type`.

The `owner` hash table is optional and can be used to meet our billing address requirements. You can provide the owner information, including the address when creating a secondary source.&#x20;

{% hint style="info" %}
We recommend that you do not provide an [owner object](../payments-solutions/digitalriver.js/payment-methods/common-payment-objects.md#owner-object) with the secondary source. This ensures that the wrong address is not applied to the cart which will trigger a payment auth failed error.
{% endhint %}

The `upstreamId` parameter is useful for mapping the source to your credit management system.

{% tabs %}
{% tab title="POST/sources request" %}
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
{% endtab %}
{% endtabs %}

A `201 OK` response returns a unique [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) in a [`chargeable` state](./#source-state). You should [attach it to a cart](using-the-source-identifier.md#attaching-sources-to-a-cart) so that we can use it to generate a one-time charge.

{% tabs %}
{% tab title="POST/sources response" %}
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
{% endtab %}
{% endtabs %}

## Combining primary and secondary payment sources

You can associate a [primary payment source](using-the-source-identifier.md#primary-payment-sources) with only one [secondary payment source](using-the-source-identifier.md#secondary-payment-sources).

In the Cart API, the following payment methods support the use of `customerCredit`: [Credit Cards](../payments-solutions/digitalriver.js/payment-methods/credit-cards.md),  [Google Pay](../payments-solutions/digitalriver.js/payment-methods/google-pay.md), [Klarna](../payments-solutions/digitalriver.js/payment-methods/klarna.md), [PayPal Express Checkout](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-express-checkout-digital-wallet), [PayPal Credit](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-credit), [PayPal Billing Agreement](../payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-billing-agreement), and Wire Transfer.

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

1. Send the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a secondary source.
2. Send the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a primary source.

#### Best practice 2: Use /apply-payment-method and /apply-shopper

Use the following steps only for authenticated shoppers.

1. Send the [POST /apply-payment-method](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to attach a secondary source
2. Send the  [`POST /apply-shopper`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post) request to attach the primary source. The default payment option saved to the shopper will be applied to the cart when applying a shopper. Note that the shopper can only save the primary source to their account.

### Address information

When you attach a source to the cart using the [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-or-Detach-Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) and the cart already has address information, the system will not use the `source` address. It will use the existing address in the cart. If the cart does not have the address information, the system will copy the address from the `source` to the cart.&#x20;

This behavior applies to both primary and secondary sources. This is why we recommend that you don't include the owner information when you [create a secondary source](using-the-source-identifier.md#creating-secondary-sources).

When you attach a source to a shopper using [`POST /payment-options`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post), the system will save the source's payment information and address to the shopper's payment options, and associate the address with the payment. When you apply a shopper to a cart using [`POST /apply-shopper`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post), the system will apply the shopper's default payment method and copy the address associated with the payment method to the card, regardless of whether the cart has an address available or not.

### Amount contributed from each payment source

After applying the payment source to the cart, the amount contributed by the payment source appears in the `amountContributed` field for the `paymentMethod` object in the /cart, /submit-cart, and /order responses.

{% code title="Single payment example" %}
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

{% code title="Two payment methods example" %}
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
* `amountRemainingToBeContributed`: indicates the gap amount required to fulfill the order. If the value is not zero that means the shopper should apply an additional payment to the cart to cover the order total amount.

{% code title="paymentSession example" %}
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

* `DELETE v1/shoppers/me/carts/active/apply-payment-method` removes a payment source from the cart. Use this option and include the source ID in the payload to remove payment sources one by one.
* `DELETE v1/shoppers/me/carts/active/payment` removes all attached sources directly from the cart

When finished, you can [attach new sources](using-the-source-identifier.md#attaching-multiple-sources-to-the-cart) to the cart.

### Refunds

If a customer requests a refund, the system will refund the [primary payment source](using-the-source-identifier.md#primary-payment-sources) first. Once the system fully refunds the primary source, the system will use the [secondary payment source](using-the-source-identifier.md#secondary-payment-sources) to refund the remaining value.&#x20;

For example, a customer purchased a line item quantity of 10 for a total of $1000. They used $600 from their primary payment source (for example, a credit card) and $400 from their secondary payment source (for example, store credit) to pay for the order. If the customer requests a refund of $400, the system refunds $400 to their credit card. If the customer requests a refund of $700, the system refunds $600 to their credit card and $100 to their store credit.

## Charging a single-use payment source

Your storefront may be configured so that customers are not required to create an account or sign-in to make a purchase. In this case, after you submit the guest customer's payment details, [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/) will [create a Source](../../general-resources/reference/digitalriver-object.md#createsource-sourcedata) and return the `sourceId` .  You can then use a [`POST /apply-payment-method`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Payment-Method/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-payment-method/post) request to set the `sourceId` attribute.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://<<host>>/v1/shoppers/me/carts/active/apply-payment-method' \
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



## Switching the default payment source

Registered customers may have multiple saved payment methods associated with their account. These Source objects are stored in the `sources` array of the [Payment Options](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options) resource.&#x20;

The first Source attached to a Customer becomes the default payment method where `isDefault` is set to `true` and its identifier is assigned to the `sourceId` attribute. If you'd like to assign a different payment method as the default, simply submit a [`POST /payment-options/{id}`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Payment-Options/paths/\~1v1\~1shoppers\~1me\~1payment-options/post) request where `{id}` is the new default payment method and set `isDefault` to `true`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
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
{% endtab %}
{% endtabs %}
