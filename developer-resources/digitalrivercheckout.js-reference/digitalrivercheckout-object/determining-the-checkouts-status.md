---
description: Learn how to check the status of a Prebuilt Checkout
---

# Determining the checkout's status

The [`DigitalRiverCheckout` object](./) exposes `getStatus()`. This function can be used to determine the status of a [Prebuilt Checkout](../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window).

```javascript
const status = drCheckout.getStatus();
```

The function returns a `status` that indicates the state of the `modal` and the customer’s `currentStep` in the experience:

```json
{
    "status": {
        "modal": "active",
        "currentStep": "addressInfo"
    }
}
```

## `modal`

The following are the possible `modal` status values:

* `pending`: The [checkout-session identifier](../../../integration-options/low-code-checkouts/drop-in-checkout.md#the-checkout-session-identifier) has not yet been created
* `inactive`: The checkout-session identifier has been created and the modal is initialized
* `active`: The [modal window](../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) is displayed to the customer
* `failed`: The modal window cannot be displayed to the customer
* `aborted`: The customer closed the modal window
* `finished`: The customer successfully provided payment and submitted the order&#x20;

## `currentStep`

The following are the possible `currentStep` values:

* `addressInfo`: The customer is in the [address information collection stage](../../../integration-options/low-code-checkouts/drop-in-checkout.md#name-and-address)
* `shippingChoice`: The customer is in the [shipping choice selection stage](../../../integration-options/low-code-checkouts/drop-in-checkout.md#shipping-choice)
* `paymentDetails`: The customer is in the [payment collection stage](../../../integration-options/low-code-checkouts/drop-in-checkout.md#payment)
