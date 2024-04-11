---
description: Gain a better understanding of how to define a checkout-session
---

# Checkout-sessions

A [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) determines what information and options are presented to customers in [low-code checkouts.](../../integration-options/low-code-checkouts/)

At a minimum, your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) needs to contain [currency](checkout-sessions.md#currency) and [product data](checkout-sessions.md#product-data).

You can also tell us whether your prices are [tax inclusive](checkout-sessions.md#tax-inclusive).&#x20;

If the customer’s cart contains [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), make sure to provide [shipping method options](checkout-sessions.md#shipping-methods) for customers to select from.&#x20;

When checking out [registered customers](checkout-sessions.md#registered-customers), you can send their [unique identifier](checkout-sessions.md#customer-identifier) and their [saved addresses](checkout-sessions.md#saved-addresses).&#x20;

For complete specifications, refer to the [checkout-sessions API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) reference docs.

## Upstream identifier

In `upstreamId`, you can pass the unique identifier of the order in your system. If `upstreamId` is not `null`, then [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md) displays its value as the order number during the [thank you stage](../../integration-options/low-code-checkouts/drop-in-checkout.md#order-confirmation).

<figure><img src="../../.gitbook/assets/upstreamId in order confirmation.png" alt=""><figcaption></figcaption></figure>

## Currency

You need to pass `currency` in your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession). This value determines how amounts are denominated in the checkout experience.

## Language

To control how the checkout experience, purchase invoices, and credit memos are localized, you can pass `language` in [create checkout-session requests](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

For a list of accepted values, refer to [Supported languages](../supported-languages.md).

{% hint style="info" %}
If you define [`options.language`](../digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#localize-the-modal) in [Prebuilt Checkout's configuration object](../digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/), that value gets assigned to the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `language`.
{% endhint %}

Digital River uses the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `language` to set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `language`, which, once the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is successfully created, determines [how purchase invoices and credit memos are localized](../../integration-options/checkouts/creating-checkouts/designating-a-locale.md).&#x20;

## Product data

For each product in the customer’s cart, you'll need to use `items[]` to send its:

* `skuId` or `productDetails`. For details, refer to [Product basics](../../product-management/skus.md).
* `price` or `aggregatePrice`. For details, refer to [Setting product price](../../integration-options/checkouts/creating-checkouts/describing-the-items/#setting-price-and-quantity).&#x20;
* `quantity`

```json
{
  "currency": "USD",
  "items": [
    {
      "skuId": "3ea112ec-83b6-45c7-8e22-e2114e903745",
      "quantity": 1,
      "price": 300
    }
  ],
  ...
}
```

You can also use `items[]` to provide:

* [`subscriptionInfo`](checkout-sessions.md#subscription-information).&#x20;
* a [`shipFrom`](checkout-sessions.md#ship-from) location.
* a `discount` on the product
* a [`strikeThroughPrice`](checkout-sessions.md#strike-through-price) that highlights how much customers are saving

### Subscription information

If you're using an external subscription service, and would like the billing frequency of the subscription that the customer is acquiring to be displayed in the checkout experience, then specify a `plan.interval` and `plan.intervalCount` in `items[].subscriptionInfo` of your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).

{% hint style="success" %}
For details on how to configure a [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) for use with [Digital River's subscription service](../../using-our-services/subscriptions.md), refer to [Processing subscription acquisitions](../../integration-options/low-code-checkouts/processing-subscription-acquisitions.md).
{% endhint %}

```
curl --location 'https://api.digitalriver.com/drop-in/checkout-sessions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret API key>' \
--header 'Cookie: incap_ses_1534_1638494=XqzQWfBdTnr/Iulkbd1JFRgmMGUAAAAATAFsJGY9H4p0aPzzfZ+ABg==; nlbi_1638494_1914372=rwWKAgHbKVXvxmI9vwbRrQAAAADFueEsAnIupi3c6RgUhNET; visid_incap_1638494=ZgPNr8DiSPety37xbpnVqijUnmQAAAAAQUIPAAAAAAC6uhinP72rh9xkXa7aYFH+' \
--data-raw '{
    ...
    "items": [
        {
            ...
            "subscriptionInfo": {
                "plan": {
                    "interval": "month",
                    "intervalCount": 1
                }
            }
        }
    ],
    ...
}'
```

Digital River reads those values and displays them in the order summary section of [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md).

{% hint style="warning" %}
This feature is not yet supported in [Components](../../integration-options/low-code-checkouts/implementing-a-components-checkout.md).
{% endhint %}

<figure><img src="../../.gitbook/assets/billing frequency.png" alt=""><figcaption></figcaption></figure>

Additionally, if you need this data to populate [email notifications](../../order-management/customer-notifications.md), or some other potential use case, then we also add these key-value pairs to the [`event`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).

### Strike through price

To highlight how much customers are saving when purchasing a product, you can send `items[].strikeThroughPrice`. The value you assign this parameter in a [create checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) request typically represents the original, pre-discounted price of an `items[]`, which Digital River then crosses out and displays next to the discounted `price`.

{% tabs %}
{% tab title="Create checkout-sessions request" %}
```
curl --location 'https://api.digitalriver.com/drop-in/checkout-sessions' \
...
--data-raw '{
  ...
  "items": [
    {
      ...
      "quantity": 1,
      "price": 100,
      "strikeThroughPrice": 125
    }
  ],
  ...
}
```
{% endtab %}

{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Components" %}
{% hint style="info" %}
The [order summary component](../digitalrivercheckout.js-reference/digitalrivercheckout-object/components/order-summary-component.md) currently doesn't support this feature.&#x20;
{% endhint %}
{% endtab %}
{% endtabs %}

Other parameters in the request don't affect how `strikeThroughPrice` is rendered in the checkout experience. Digital River displays its value _as is_. For example, we don't adjust it depending on the [`taxInclusive`](checkout-sessions.md#tax-inclusive) setting. &#x20;

So, if an `items[]` has a `quantity` that's greater than `1`, and you're trying to communicate a discount, make sure you implement pre-request logic that ensures `strikeThroughPrice` is less than `price` multiplied by `quantity`. Otherwise, it will appear that the product's price is being marked-up, instead of discounted.&#x20;

The parameter is not intended for use with either `discount` or `items[].discount` since this might result in conflicting information getting displayed in the experience. &#x20;

If you're using the [local pricing service](../../using-our-services/local-pricing.md), then we perform a currency conversion on `strikeThroughPrice`, just like we do with `price`, based on what [users have selected](../../using-our-services/local-pricing.md#local-pricing-selector) when they initiate checkout.&#x20;

## Shopping country

A [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shoppingCountry` represents the country in which a customer is based.&#x20;

If you send a `shoppingCountry` that's not `null`, Digital River uses that value to populate the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shipTo.address.country`. This is true whether [`items[]`](checkout-sessions.md#product-data) represents [physical, digital, or mixed goods](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital).

{% hint style="success" %}
You can also [save a default shopping country in Digital River Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration). If you do so, `shoppingCountry` in a [`POST /drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) overrides (but doesn't overwrite) the value saved in Dashboard.&#x20;
{% endhint %}

Additionally, `shoppingCountry` prompts Digital River to disable the shipping country drop-down menu and blocks customers from selecting any  [`options.addresses[]`](checkout-sessions.md#saved-addresses) whose `country` doesn't match `shoppingCountry`.

{% tabs %}
{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/shopping country - PBC.png" alt="" width="563"><figcaption></figcaption></figure>


{% endtab %}

{% tab title="Components" %}
<figure><img src="../../.gitbook/assets/shopping country - components.png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

However, a [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shoppingCountry` and `billTo.address.country` don't need to match. As a result, the bill to country drop-down menu remains operable and customers can choose from any [`options.addresses[]`](checkout-sessions.md#saved-addresses).&#x20;

{% tabs %}
{% tab title="POST /drop-in/checkout-sessions" %}
The following [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) passes `shoppingCountry` and its single [`items[].skuId`](checkout-sessions.md#product-data) references a [digital product](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital).

```
curl --location --request POST 'https://api.digitalriver.com/drop-in/checkout-sessions' I am running a few minutes late; my previous meeting is running over.
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <secret API key>' \
....
    "currency": "JPY",
    ...
    "items": [
        {
            "skuId": "sku-dig-subscription-01",
            "quantity": 1,
            "price": 459
        }
    ],
    "shoppingCountry": "JP",
    ...
    "options": {
        ...
        "addresses": [
            {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "line2": "line 2",
                    "city": "Minnetonka",
                    "postalCode": "55129",
                    "state": "MN",
                    "country": "US"
                },
                "name": "John Smith",
                "phone": "952-111-1111",
                "email": "jsmith@digitalriver.com",
                "organization": "Digital River"
            },
            {
                "address": {
                    "line1": "62 Trinity Crescent",
                    "line2": "",
                    "city": "WHITCHURCH",
                    "postalCode": "CF4 9ZB",
                    "country": "GB"
                },
                "name": "Brenna Brawner",
                "phone": "07854319925",
                "email": "anna@dr.com",
                "organization": "Digital River"
            }
        ]
    }
}'
```
{% endtab %}

{% tab title="Delivery information" %}
As a result, the country drop-down menu in the delivery information stage is locked.&#x20;

<figure><img src="../../.gitbook/assets/Locked drop-down.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Billing information" %}
In the billing information stage, however, the country selector remains operational.&#x20;

#### Prebuilt Checkout

<figure><img src="../../.gitbook/assets/non locked (1).png" alt=""><figcaption></figcaption></figure>

#### Components

<figure><img src="../../.gitbook/assets/shopping country - components 2.png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Events" %}
And even though [`items[]`](checkout-sessions.md#product-data) only references [digital products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), the [`checkout_session.order.created`](../../integration-options/low-code-checkouts/drop-in-checkout.md#handling-the-checkout-session-order-created-event) and `order.*` [events](../../order-management/events-and-webhooks-1/events-1/) contain `shipTo.address.country`.

{% code title="order.accepted" %}
```json
{
    "id": "6ea4f842-0da7-488b-a078-50444df607b6",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "246318070336",
            ...
            "shipTo": {
                "address": {
                    "country": "JP"
                }
            },
            ...
            "billTo": {
                "address": {
                    "line1": "123 My St",
                    "city": "Tokyo",
                    "postalCode": "100-0013",
                    "country": "JP"
                },
                ...
            },
            ...
            "items": [
                {
                    "id": "175174880336",
                    "skuId": "sku-dig-subscription-01",
                    ...
                }
            ],
            ...
        }
    },
    ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The `shoppingCountry` also plays a role in determining:

* What [address validations](../../integration-options/checkouts/creating-checkouts/providing-address-information.md#address-requirements-and-validations) a customer's inputs are subjected to.
* Whether customers are shown a form that collects their tax identification number and whether they have the option to enter a value or are required to do so.
* What options are displayed in the payment collection stage.
* The designated [selling entity](../../integration-options/checkouts/creating-checkouts/selling-entities.md), which affects what compliance disclosures get displayed and whether a [purchase invoice](../../order-management/accessing-invoices-and-credit-memos.md) is eventually generated.

## Ship from

If [`items[]`](checkout-sessions.md#product-data) contains [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), then your [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) needs to meet certain `shipFrom.address` requirements.&#x20;

For details, refer to [Ship from requirements](../../integration-options/checkouts/creating-checkouts/providing-address-information.md#ship-from-requirements) on the [Providing address information](../../integration-options/checkouts/creating-checkouts/providing-address-information.md) page. There'll you find [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) requirements, which the checkout-session wraps.

To get this data added to the checkout-session, you can:

* Send `shipFrom` in a [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;
* [Save a default ship from address in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration). If you do this, then any  `shipFrom` values sent in a [`POST /drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) override (but don't overwrite) those saved in Dashboard.&#x20;
* [Use a shipping endpoint](../../integration-options/low-code-checkouts/using-a-shipping-endpoint.md) to dynamically provide Digital River one or more `shipFrom` locations during the checkout process.

## Customer type

The [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `customerType` indicates whether customers are making the purchase as an `individual` or on behalf of a `business`.&#x20;

If `customerType` is `business`, then customers must enter their company's name in both the shipping and billing information collection forms.&#x20;

Additionally, in many cases, a value of `business` is required to activate the tax identifier collection form. For details, refer to [Supported tax identifiers](../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers).&#x20;

### Auto collect customer type

You can pass [`customerType`](checkout-sessions.md#customer-type) in a [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession). But to do so, you'll need to have this information before initiating checkout.

If you'd like Digital River to ask customers during the checkout process whether they're making the purchase on behalf of a business, then you'll need to [turn this feature on in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md) and your [`POST /drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) must (1) omit `customerType` (2) or assign a value of `individual` or `null` to this parameter.

For details, refer to:

* [B2B transactions](../../integration-options/low-code-checkouts/drop-in-checkout.md#business-to-business-transactions) in [Name and address stage](../../integration-options/low-code-checkouts/drop-in-checkout.md#name-and-address) on the [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md) page
* [Business to business transactions](../digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md#business-to-business-transactions) on the [Address Component](../digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md) page.

## Tax inclusive

The `taxInclusive` boolean determines how we treat product prices when calculating tax.

It also dictates how prices are displayed in the checkout experience. The default value is `false`. If you set `taxInclusive` to `true`, then the experience indicates that the total amount includes VAT.

## Registered customers

For checkouts initiated by a registered customer, your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) can include the following:

* [A customer identifier](checkout-sessions.md#customer-identifier)
* [Saved addresses](checkout-sessions.md#saved-addresses)

### Customer identifier

To checkout customers registered in your system, send their `customerId`.

```json
{
  ...
  "customerId": "230f61be-8822-4325-9926-e9d0731691b4"
  ...
}
```

Digital River uses this value to determine whether a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) with that identifier exists in our system.

If it does, we retrieve that [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) transaction-applicable [`taxIdentifiers[]`](../../integration-options/checkouts/creating-checkouts/tax-identifiers.md) and payment [`sources[]`](../../payments/payment-sources/) and, for convenience purposes, present them as options in the tax identifier and payment collection forms.

If the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) doesn’t yet exist in our system, we create a new object and assign it the `customerId` you provided.

In either case, as registered customers progress through a [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md), they are given the option to save their shipping information, tax identifiers and billing information for use in future transactions. In both [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md) and [Components](../../integration-options/low-code-checkouts/implementing-a-components-checkout.md), they can do the same for their selected payment method.

### Saved addresses

If you persist registered customers’ addresses, and the customer checking out has one or more saved values in your system, you can use `options.addresses[]` to send Digital River this data.

```json
{
  ...
  ...
  "options": {
  ...
    "addresses": [
      {
        "address": {
          "line1": "10380 Bren Rd W",
          "city": "Minnetonka",
          "postalCode": "55129",
          "state": "MN",
          "country": "US"
        },
        "name": "John Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com",
        "organization": "Digital River",
        "additionalAddressInfo": {
          "neighborhood": "Centro",
          "division": "営業部",
          "phoneticName": "ヤマダ タロ"
        }
      },
      {
        "address": {
          "line1": "62 Trinity Crescent",
          "city": "WHITCHURCH",
          "postalCode": "CF4 9ZB",
          "country": "GB"
        },
        "name": "Anna Brawner",
        "phone": "07854319925",
        "email": "anna@dr.com",
        "organization": "Digital River",
        "additionalAddressInfo": {
          "neighborhood": "Centro",
          "division": "営業部",
          "phoneticName": "ヤマダ タロ"
        }
      }
    ]
  },
  ...
}
```

In the address collection stage, we present these saved values to customers for convenience purposes.

{% hint style="info" %}
For each `options.addresses[]`, Digital River only displays its `name` and `address`.
{% endhint %}

## Shipping methods

If [`items[]`](checkout-sessions.md#product-data) contain [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), you must provide Digital River shipping options for customers to select from. You can do this in one of the following ways:

First, you can send `options.shippingMethods[]` in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

Alternatively, you can [save default shipping methods in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration). These represent static options (i.e., ones whose `amount` and `serviceLevel` are not dependent on where the products are being shipped or how much they weigh). If you use this approach,  `options.shippingMethods[]` sent in the [create checkout-session request](../../integration-options/low-code-checkouts/drop-in-checkout.md#creating-a-checkout-session) override (but do not overwrite) your saved values in Dashboard.&#x20;

Finally, you can [set up a shipping endpoint](../../integration-options/low-code-checkouts/using-a-shipping-endpoint.md) that Digital River calls at checkout time. This lets you offer your customers dynamic options in the shipping method selection stage. The data returned by this endpoint overrides any `options.shippingMethods[]` sent in your request or saved in Dashboard.&#x20;

For each of the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions)  `options.shippingMethods[]`, the checkout experience's shipping choice selection form displays its `amount`, `description`, `serviceLevel`, and [`shippingTerms`](../../general-resources/glossary.md#shipping-terms).&#x20;

```json
{
  ...
  "options": {
    "shippingMethods": [
      {
        "amount": 5,
        "description": "Standard Shipping",
        "serviceLevel": "SG"
      },
      {
        "amount": 15,
        "description": "Next Day Air",
        "serviceLevel": "ND"
      }
    ],
    ...
  },
  ...
}
```

{% hint style="success" %}
Each `options.shippingMethods[]` requires an `amount` but not a `serviceLevel`. However, this data helps Digital River detect fraud, so we highly encourage you to pass it.&#x20;
{% endhint %}

If you submit a [`POST /drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) with physical [`items[]`](checkout-sessions.md#product-data) but without  `options.shippingMethods[]`, and you don't have [default shipping methods](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration) or a [shipping callout endpoint](../../administration/dashboard/settings/prebuilt-checkout.md#configure-a-shipping-callout) saved in Dashboard, then the request returns the following error:

{% code title="400 Bad Request" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_request",
            "message": "Shipping methods are required with physical items"
        }
    ]
}
```
{% endcode %}

## Store credits

In the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), `options` allows you to pass one or more `storeCredits[]`. Each element in this array can be defined by an [`amount`](checkout-sessions.md#amount), [`name`](checkout-sessions.md#name), [`upstreamId`](checkout-sessions.md#upstreamid), [`iconUrl`](checkout-sessions.md#iconurl), and [`lastFour`](checkout-sessions.md#lastfour).&#x20;

{% hint style="info" %}
In the payment collection forms, we display `amount`, `name`, `iconUrl` and `lastFour` to customers.&#x20;
{% endhint %}

For more details, refer to [Offering store credit](../../integration-options/low-code-checkouts/offering-store-credit.md).&#x20;

```
curl --location --request POST 'https://api.digitalriver.com/drop-in/checkout-sessions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Secret API key>' \
....
--data-raw '{
    ...
    "options": {
        ...
        "storeCredits": [
            {
                "amount": 5,
                "name": "Acme Inc.",
                "upstreamId": "7654-2345-0987-123456",
                "iconUrl": "https://acme-inc.com/store-credit-log.png",
                "lastFour": "7831"
            }
        ]
    }
}'
```

#### `amount`

This required parameter represents how much credit you’re offering the customer.&#x20;

#### `name`

The name of the store credit offering. Omitting `name` or passing a `null` value doesn't throw an [error](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-types), but it does mean that that particular `storeCredits[]` won't get displayed in the payment collection form.&#x20;

#### `upstreamId`

This required parameter uniquely identifies the line of credit in your system. Passing multiple `storeCredits[]` that share the same `upstreamId` is not allowed.

{% code title="400 Bad Request" %}
```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "options.storeCredits",
            "message": "Unique value required for upstreamId."
        }
    ]
}
```
{% endcode %}

#### `iconUrl`

The web address of your store credit logo.&#x20;

#### `lastFour`

The last four digits of the customer's store credit card.&#x20;

## Style

You can control the appearance and visual behavior of a [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) by defining `style` in a [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

For details, refer to [Defining experience](../digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/defining-experience.md).&#x20;
