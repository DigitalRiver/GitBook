---
description: >-
  Gain a better understanding of the thank your component along with how to
  create and mount it
---

# Thank you component

The thank you component confirms that the purchase was successful and displays the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) identifier.&#x20;

![](<../../../../.gitbook/assets/Thank you element.png>)

The component can also display instructions on authorizing [Konbini](../../../../payments/supported-payment-methods/konbini.md), [Wire Transfer](../../../../payments/supported-payment-methods/wire-transfer.md), and other delayed payment methods. More specifically, if the [`flow`](../../../../payments/payment-sources/#authentication-flow) of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [primary `payment.sources[]`](../../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) is `receiver`, then the component provides customers guidance on how to push the funds.&#x20;

![](<../../../../.gitbook/assets/thank you element - delayed payment instructions.png>)

Refer to [Handling success events](../../../../integration-options/low-code-checkouts/implementing-a-components-checkout.md#success-events) on the [Components checkout](../../../../integration-options/low-code-checkouts/implementing-a-components-checkout.md) page for details on determining when to display this component.&#x20;

## Creating the thank you component

To create an instance of the thank you component, pass `'thankyou'` to [`createComponent()`](./#createcomponent-componenttype).

```javascript
let thankYouComponent;
...
thankYouComponent = components.createComponent('thankyou');
...
```

## Mounting the thank you component

To attach the thank you component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).&#x20;

```javascript
<div id="order-details-container" style="display: block">
...
thankYouComponent.mount('order-details-container');
...
```
