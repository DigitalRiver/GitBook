---
description: >-
  Gain a better understanding of the invoice component, how to create and mount
  it, as well as how to submit the information it collects from customers
---

# Invoice component

The invoice component collects information needed to comply with Taiwan's e-invoicing requirements. For background on these requirements, refer to [e-Invoicing](../../../../using-our-services/e-invoicing.md).&#x20;

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (103).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

To use the component, you'll need to [create it](invoice-component.md#creating-the-invoice-component), [mount it](invoice-component.md#mounting-the-invoice-component), and [submit its data](invoice-component.md#submitting-the-invoice-component).

In the `data` returned by [`onChange`](configuring-components.md#onchange), you can use [`showInvoiceAttribute`](configuring-components.md#showinvoiceattribute) to determine whether this component must be displayed.

## Creating the invoice component

To create an instance of the invoice component, pass `'invoiceattribute'` to [`createComponent()`](./#createcomponent-componenttype).&#x20;

```javascript
let invoiceComponent;
...
invoiceComponent = components.createComponent('invoiceattribute');
```

## Mounting the invoice component

To attach the invoice component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).

```javascript
<div id="invoice-container" style="display: block"></div>
...
invoiceComponent.mount('invoice-container');
```

## Submitting the invoice component

The invoice component exposes `done()`, which submits the customer's input and returns a boolean. It requires that you use the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator and, therefore, must be called inside an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function).

```javascript
const invoiceComponentStatus = await invoiceComponent.done();
```

If `done()` returns `true`, this indicates that customers entered a properly formatted carrier value, and your code can advance them to the next stage of the checkout. &#x20;

A `false` value indicates that customers either didn't provide a value or it's incorrectly formatted, and you shouldn't allow the checkout to advance. In this case, the component prompts customers to try again and offers them formatting assistance.

<figure><img src="../../../../.gitbook/assets/image (115).png" alt="" width="563"><figcaption></figcaption></figure>
