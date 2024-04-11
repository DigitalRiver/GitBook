---
description: Learn how to add custom fields to a Prebuilt Checkout
---

# Adding custom fields

If you’d like to collect additional information from customers during a [low-code checkout](./), you can add custom fields to the experience.

Digital River adds what these fields contain to the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) so that you can use it in downstream processes.

## Setup custom fields

On [Digital River Dashboard’s Prebuilt Checkout page](../../administration/dashboard/settings/prebuilt-checkout.md), you can configure a maximum of two custom fields, each of which can accept a number, text (i.e., string), or a set of pre-defined drop-down options.

<figure><img src="../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

For each field, you need to:

* Indicate whether it’s required or optional.&#x20;

{% hint style="warning" %}
If you mark it as required, then express checkout is disabled in [Prebuilt Checkout](drop-in-checkout.md).
{% endhint %}

* Define a unique key and make sure it contains no whitespaces.
* Define a label that will be displayed to customers in the experience.

If you’re using the drop-down field, you’ll also need to enumerate a list of acceptable values, along with a display label for each.

## The checkout experience

Depending on whether you add [physical or digital-only products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) to the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) [`items[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data), Digital River renders your custom fields in the shipping information or billing information form, respectively.

{% tabs %}
{% tab title="Prebuilt Checkout" %}
#### Physical products in `items[]`

<figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

#### Digital only products in `items[]`

<figure><img src="../../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Address Component" %}
#### Physical products in `items[]`

<figure><img src="../../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

#### Digital only products in `items[]`

<figure><img src="../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

If you marked a field as required, and customers don't provide a value, they are prompted for an input.&#x20;

{% tabs %}
{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Address Component" %}
<figure><img src="../../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

Number only fields provide help text if customers enter a non-digit character.

{% tabs %}
{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Address Component" %}
<figure><img src="../../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

Number and text fields accept values with a maximum length of 500 characters.

Labels aren't translated into the [`language`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#language) of the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions), but instead default to English.

## Implement custom fields in Components

The [`done()`](implementing-a-components-checkout.md#submitting-components) function, which submits the data collected by the [address component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md) in an update [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) request, returns `false` if the user (1) fails to enter a value in a custom field that you marked as required or (2) enters a value that exceeds 500 characters in a custom number or text field.

If your application is setup correctly, this should block customers from proceeding to the checkout's next stage.

For details, refer to [Controlling the checkout flow](implementing-a-components-checkout.md#controlling-the-checkout-flow).&#x20;

If you [mark a custom field as required in Dashboard](adding-custom-fields.md#setup-custom-fields), then you might want to disable the [wallet component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/wallet-component.md). When users click a button in this component, they're redirected to a payment provider. But the form in the provider's interface doesn't contain a field to collect your custom data, and, as a result, it won't get added to the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md). &#x20;

## Retrieve the collected data

After customers successfully submit the form, Digital River adds the key and value of each field they completed to the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `metadata`.

You can access this data by:

* [Configuring a webhook](../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for certain [types](../../order-management/events-and-webhooks-1/events-1/#event-types) of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events), such as [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created), [`order.accepted`](../../order-management/events-and-webhooks-1/events-1/event-types.md#order.accepted), [`fulfillment.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#fulfillment.created), `order.fulfilled`, and [`order.refunded`](../../order-management/events-and-webhooks-1/events-1/event-types.md#order.refunded).

{% tabs %}
{% tab title="order.accepted" %}
```json
{
    "id": "66524f24-74d5-4356-b30f-ff1da95db3eb",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "295121620336",
           ...
            "metadata": {
                "freeSample": "chewToy",
                "giftCardMessage": "A special treat for Zoey's birthday"
            },
            ...
        }
    },
    ...
}
```
{% endtab %}

{% tab title="fulfillment.created" %}
{% code title="Event" %}
```json
{
    "id": "9baea62d-cec5-49e1-b8ac-8546b2007e8d",
    "type": "fulfillment.created",
    "data": {
        "object": {
            "id": "ful_854dee4b-cf4b-43b9-aecb-89d46a9f96cf",
            ...
            "orderDetails": {
                "id": "295121620336",
                ...
                "metadata": {
                    "freeSample": "chewToy",
                    "giftCardMessage": "A special treat for Zoey's birthday"
                },
                ...
            }
        }
    },
   ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

* Assigning a callback to [`onCheckoutComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#oncheckoutcomplete) in [Prebuilt Checkout's configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/) and then implementing a handler.
* Assigning a callback to [`onSuccess`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#success-event) in the [Component's configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md) and then implementing a handler.&#x20;
* Making a call to [retrieve the order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders/operation/retrieveOrders).

Once you have this `metadata`, you can use it to populate email notifications, fulfill an order’s goods, or perform other operations of your choice.
