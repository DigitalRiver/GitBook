---
description: >-
  Learn how to configure a checkout button that can be used to create a Prebuilt
  Checkout modal
---

# Rendering a checkout button

The [`DigitalRiverCheckout` object](../) exposes `renderButton()`, which allows you to define a checkout button's location, style, and text. It can also hide existing buttons and initiate the creation of a [Prebuilt Checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window).

The function accepts two parameters, a [button container](./#button-container) and [button options](./#button-options).

```javascript
digitalRiverCheckout.renderButton(buttonContainer, buttonOptions);
```

## Button container

The required button container represents the `id` of an [HTML element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) in which you want [DigitalRiverCheckout.js](../../) to render your checkout button.

```javascript
<div id="button-container"></div>
...
const buttonContainer = '#button-container';
```

## Button options

In button options, you can:

* [Style the button](./#style-the-button)
* [Customize the button's text](./#customize-the-buttons-text)
* [Hide elements](./#hide-elements)
* [Add the button to the DOM](./#after-button-render-actions)
* Define how you'd like to handle:
  * [Button initialization events](./#button-initialization-event)
  * [Button click events](./#button-click-event)&#x20;
  * [Checkout cancel events](./#checkout-cancel-event)

```javascript
const buttonOptions = {
  style: {
    backgroundColor: '#B52',
    borderRadius: '4px',
    color: '#fff',
    fontSize: '1rem',
    fontWeight: '400',
    fontFamily: 'Montserrat,Arial,Helvetica,sans-serif',
    ':hover': {
      color: 'rgb(0, 167, 225)'
    }
  },
  buttonText: 'Proceed to checkout',
  hiddenElement: ['.cart-actions > a.button', '.previewCartAction-checkout > a.button'],
  afterRender: false,
  onInit: (actions) => {},
  onClick: async (actions) => {
    try {
      actions.loading.start();
      const checkoutSessionId = await createCheckoutSession();
      actions.loading.stop();
      if (!checkoutSessionId) {
        return;
      }
      const modalConfig = getConfigObj();
      actions.checkout.modal.open(checkoutSessionId, modalConfig);
    } catch (error) {
      actions.loading.stop();
    }
  },
  onCancel: () => {}
};
```

### Style the button

The `style` object can be used to define the visual appearance of a checkout button:

* `backgroundColor`: Sets the background color
* `borderRadius`: Determines the roundness of the button's corners&#x20;
* `color`: Sets the color of the text
* `fontSize`: Sets the font size of the text
* `fontWeight`: Sets the font weight of the text
* `fontFamily`: Specifies the button's font family. If the browser doesn't support the first font, it moves through the list, from left to right, looking for one it does.
* `':hover'`: This object contains a nested `color` property which determines the color of the button when it's hovered over.&#x20;

```javascript
const buttonOptions = {
  style: {
    backgroundColor: '#B52',
    borderRadius: '4px',
    color: '#fff',
    fontSize: '1rem',
    fontWeight: '400',
    fontFamily: 'Montserrat,Arial,Helvetica,sans-serif',
    ':hover': {
      color: 'rgb(0, 167, 225)'
    }
  },
  ...
};
```

### Customize the button's text

The `buttonText` allows you to customize the characters displayed on the button. The default value is `Check out`.&#x20;

```javascript
const buttonOptions = {
  ...
  buttonText: 'Proceed to checkout',
  ...
};
```

### Hide elements

The `hiddenElement` array represents one or more [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_Selectors) strings that you want [DigitalRiverCheckout.js](../../) to locate and then hide before rendering the checkout button. This allows you to conceal add to cart, cart preview, and similar buttons that might exist on the page.

```javascript
const buttonOptions = {
  ...
  hiddenElement: ['.cart-actions > a.button', '.previewCartAction-checkout > a.button'],
  ...
};
```

In the example, `'.cart-actions > a.button'` and `'.previewCartAction-checkout > a.button'` target elements that have a `class` value of `"button"` and are descendants of elements with classes of `"cart-actions"` and `"previewCartAction-checkout"`, respectively.

### After button render actions

The `afterRender` boolean determines whether or not the [button container](./#button-container) gets dynamically added to the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model/Introduction).

```javascript
const buttonOptions = {
  ...
  afterRender: false,
  ...
};
```

### Button initialization event

The `onInit` property can be assigned a callback method, which accepts [`actions`](performing-actions-on-the-checkout-button.md), that executes when the checkout button first renders.&#x20;

```javascript
const buttonOptions = {
  ...
  onInit: (actions) => {},
  ...
};
```

### Button click event

The `onClick` property can be assigned a callback method, which accepts [`actions`](performing-actions-on-the-checkout-button.md), that executes when the user clicks the checkout button.

```javascript
const buttonOptions = {
  ...
  onClick: async (actions) => {
    try {
      actions.loading.start();
      const checkoutSessionId = await createCheckoutSession();
      actions.loading.stop();
      if (!checkoutSessionId) {
        return;
      }
      const modalConfig = getConfigObj();
      actions.checkout.modal.open(checkoutSessionId, modalConfig);
    } catch (error) {
      actions.loading.stop();
    }
  },
  ...
};
```

In most cases, to handle this event, you'll define an asynchronous function that creates a [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) and then passes its identifier to [`actions.checkout.modal.open()`](performing-actions-on-the-checkout-button.md#open-a-checkout-modal).&#x20;

For details, refer to [Setting up the shopping experience](../../../../integration-options/low-code-checkouts/offering-local-pricing.md#setting-up-the-shopping-experience) on the [Offering local pricing](../../../../integration-options/low-code-checkouts/offering-local-pricing.md) page.

### Checkout cancel event

The `onCancel` property can be assigned a callback method that executes when users close the [Prebuilt Checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) before completing the purchase.

```javascript
const buttonOptions = {
  ...
  onCancel: () => {}
};
```

{% hint style="info" %}
The [`onClose`](../configuring-prebuilt-checkout/#onclose) property in the [configuration object](../configuring-prebuilt-checkout/) also allows you to listen for modal closed events.&#x20;
{% endhint %}

&#x20;
