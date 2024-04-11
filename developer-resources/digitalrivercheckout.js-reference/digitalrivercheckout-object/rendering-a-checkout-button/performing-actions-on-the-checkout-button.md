---
description: >-
  Gain a better understanding of how to perform customized actions on the
  Prebuilt Checkout button
---

# Performing actions on the checkout button

Various callback functions can be assigned to properties in the [button options configuration object](./#button-options). Some of these functions accept an optional `actions` parameter, which allows you to:

* [Start and stop a spinner](performing-actions-on-the-checkout-button.md#start-and-stop-a-loading-spinner)
* [Open a checkout modal](performing-actions-on-the-checkout-button.md#open-a-checkout-modal)

{% hint style="info" %}
Some callbacks in the [Prebuilt Checkout configuration object](../configuring-prebuilt-checkout/) also accept `actions`. For details, refer to [Performing actions on the modal.](../configuring-prebuilt-checkout/performing-actions.md)&#x20;
{% endhint %}

## Start and stop a loading spinner

The `actions` parameter exposes `loading.start()` and `loading.stop()`. These two functions display and hide a spinning GIF, a visual cue that the [checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) is in the process of opening. &#x20;

```javascript
onClick: async (actions) => {
  ...
    actions.loading.start();
    const checkoutSessionId = await createCheckoutSession();
    actions.loading.stop();
  ...
}
```

## Open a checkout modal

The `actions` parameter exposes `checkout.modal.open()`, which accepts a required [checkout-session](../../../digital-river-api-reference/checkout-sessions.md) `id` and an optional [configuration object](../configuring-prebuilt-checkout/), and results in the creation of a [checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window).

{% hint style="info" %}
The `actions.checkout.modal.open()` function accepts the same inputs and generates the same output as [`createModal()`](../#create-an-instance-of-the-checkout-modal).
{% endhint %}

For details, refer to [Button click event](./#button-click-event) on the [Rendering a checkout button](./) page.

```javascript
onClick: async (actions) => {
      ...
      actions.checkout.modal.open(checkoutSessionId, modalConfig);
      ...
  }
```
