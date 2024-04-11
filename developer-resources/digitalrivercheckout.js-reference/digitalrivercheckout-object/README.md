---
description: Learn about the functionality exposed by the DigitalRiverCheckout object
---

# DigitalRiverCheckout object

Once you [initialize DigitalRiverCheckout.js](../initializing-digitalrivercheckout.js/), you can use the `DigitalRiverCheckout` object to:

* [Create an instance of a Prebuilt Checkout](./#create-an-instance-of-a-prebuilt-checkout)
* [Create an instance of Components](./#creating-an-instance-of-components)
* [Display a checkout button](./#display-the-checkout-button)
* [Determine the modal's status](./#determine-the-status-of-the-modal)

## Create an instance of a Prebuilt Checkout

The `DigitalRiverCheckout` exposes the [`createModal()`](./#createmodal-checkoutsessionid-config) and [`embed()`](./#embed-checkoutsessionid-config) functions, either of which can be used to create an interface that customers use to checkout.

### `createModal(checkoutSessionId, config)`

This function creates an instance of a  checkout modal window, a graphical control element that appears in front of the other content on the page. When displayed, the user’s interaction with your content is temporarily disabled, and they must engage with the modal by either completing checkout or closing the window.

The function accepts a [checkout session identifier](./#checkout-session-identifier) and a [configuration object](./#configuration). &#x20;

```javascript
document.getElementById('YOUR_CHECKOUT_BUTTON_ID').addEventListener('click', async (event) => {
  
   //Invokes a client defined function that creates a checkout session
   const checkoutSessionId = await createCheckoutSession();
  
   // Creates and opens Prebuilt Checkout in a modal window
   drCheckout.createModal(checkoutSessionId, config);
})
```

### `embed(checkoutSessionId, config)`

This function creates an [Inline Frame element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) and adds [Prebuilt Checkout](../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) to it, thereby allowing you to embed the entire checkout process directly into your website.

The function accepts a required [checkout session](../../digital-river-api-reference/checkout-sessions.md) identifier and an optional [configuration object](configuring-prebuilt-checkout/). However, if you want Digital River to add the `iframe` to a specific HTML element, you'll need to define [`containerElementId`](configuring-prebuilt-checkout/#designating-a-container-for-an-inline-frame) in the configuration object.&#x20;

```javascript
document.getElementById('YOUR_CHECKOUT_BUTTON_ID').addEventListener('click', async (event) => {
  
   //Invokes a client defined function that creates a checkout session
   const checkoutSessionId = await createCheckoutSession();
  
   // Creates a Prebuilt Checkout and adds it to an iframe
   drCheckout.embed(checkoutSessionId, config);
});
```

## Creating an instance of components

The `DigitalRiverCheckout` object exposes `components()`. For details, refer to [Components](components/).

## Display the checkout button

The `DigitalRiverCheckout` object exposes `renderButton()`, which displays a checkout button that allows a customer to initiate the checkout process. For details, refer to [Rendering a checkout button](rendering-a-checkout-button/).&#x20;

## Determine the status of the modal

The `DigitalRiverCheckout` object exposes `getStatus()`, which returns data on a Prebuilt Checkout's current state. For details, refer to Determining[ the checkout's status.](determining-the-checkouts-status.md) &#x20;



