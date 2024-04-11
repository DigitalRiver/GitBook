---
description: >-
  Gain a better understanding of how to handle checkout-sessions after Digital
  River creates the order
---

# Handling completed checkout-sessions

If you're using either of our [low-code checkout solutions](./), we recommend that you [configure a webhook](../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).

This [event](../../order-management/events-and-webhooks-1/events-1/) occurs when customers complete their purchase, and Digital River converts the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). Its [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) allows you to:

* [Determine whether the customer's address information should be saved for later](handling-completed-checkout-sessions.md#determine-whether-to-save-addresses)
* [Determine what disclosures customers accepted](handling-completed-checkout-sessions.md#determine-what-disclosures-customers-accepted)
* [Access price formatting rules](handling-completed-checkout-sessions.md#access-price-formatting-rules)
* [Check whether customers used their store credit](handling-completed-checkout-sessions.md#determine-whether-customers-applied-store-credit)
* Save a copy of our [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in your database
* Retrieve `id` and add that value to the order in your system

We don’t recommend that you use `checkout_session.order.created` to trigger order fulfillment or customer notifications. Instead, listen for [`order.accepted`](../../order-management/events-and-webhooks-1/events-1/event-types.md#order.accepted) and use it to trigger downstream fulfillment processes and order confirmation emails. For details, refer to:

* [Handling accepted orders](../../order-management/creating-and-updating-an-order.md#handling-accepted-orders) on the [Processing orders](../../order-management/creating-and-updating-an-order.md) page
* [Order confirmation](../../order-management/customer-notifications.md#order-confirmation) on the [Customer notifications](../../order-management/customer-notifications.md) page

## Determine whether to save addresses

In the [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created), both `shipTo` and `billTo` contain the `saveForLater` boolean, which indicates whether customers requested that their shipping and/or billing information be saved for use in future transactions.&#x20;

```json
{
    "id": "b927e8ef-fd8e-41a5-af29-04206b24dbb8",
    "type": "checkout_session.order.created",
    "data": {
        "object": {
            "id": "262957510336",
            "checkoutId": "3a71cfd1-da2b-4378-833f-3c9ad6fcf447",
            "checkoutSessionId": "fa701918-4f4c-45a9-8f72-88064070b927",
            ...
            "shipTo": {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "city": "Minnetonka",
                    "postalCode": "55129",
                    "country": "MN"
                },
                "name": "John Smith",
                "phone": "952-111-1111",
                "email": "jsmith@digitalriver.com",
                "additionalAddressInfo": {
                    "neighborhood": "Centro",
                    "phoneticName": "ヤマダ タロ"
                },
                "saveForLater": true
            },
            ...
            "billTo": {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "city": "Minnetonka",
                    "postalCode": "55129",
                    "country": "FR"
                },
                "name": "John Smith",
                "phone": "09521111111",
                "email": "jsmith@digitalriver.com",
                "saveForLater": false
            },
            ...
        }
    },
    ...
}
```

If `true`, you can call a method that saves `address`, `name`, `phone`, `email`, and (assuming it exists) `additionalAddressInfo` in your system so that the next time this customer checks out, you can pass this data in [`options.addresses[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#saved-addresses).&#x20;

## Determine what disclosures customers accepted

The [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created) contains `consents`.&#x20;

{% hint style="info" %}
Both [`onCheckoutComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#oncheckoutcomplete) and [`onSuccess`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#success-event) also return `consents`.
{% endhint %}

```javascript
{
    "id": "1ebfd13c-4ef6-443c-b58a-cb119f1c24fd",
    "type": "checkout_session.order.created",
    "data": {
        "object": {
            "id": "1038474530082",
            ...
            "consents": {
                "termsOfService": true,
                "eula": true,
                "termsOfSale": true
            },
            ...
        }
    },
    ...
}
```

In this object, the `termsOfSale` boolean references Digital River's terms of sale. The `eula` and `termsOfService` reference your company's unique end-user license agreement and terms of service, respectively.&#x20;

{% hint style="info" %}
For details on appending your company's disclosures to ours, refer to [Create a Prebuilt Checkout configuration](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration) in the [Digital River Dashboard](../../administration/dashboard/) documentation.
{% endhint %}

If any of these attributes are `true`, it signifies that customers were presented with that specific disclosure during the payment stage and actively accepted it.&#x20;

## Access price formatting rules

For details, refer to [Access price formatting rules](offering-local-pricing.md#access-price-formatting-rules) on the [Offering local pricing](offering-local-pricing.md) page.&#x20;

## Determine whether customers applied store credit

For details, refer to [Processing store credit in orders](offering-store-credit.md#processing-store-credit-in-orders) on the [Offering store credit](offering-store-credit.md) page.&#x20;
