---
description: Learn about the functionality exposed by components
---

# Components

Components are UI building blocks that allow you to create customizable checkout flows that collect information from and present information to customers.&#x20;

On this page, you'll find information on:

* [Creating components](./#creating-components)
* [The components object](./#the-components-object)
* [The component object](./#the-component-object)

## Creating components

The [`DigitalRiverCheckout` object](../) exposes [`components()`](./#components-configuration).&#x20;

### `components(configuration)`

This function, which accepts a required [configuration object](./#the-components-configuration-object), creates [components](./#the-components-object), which you can use to manage one or more [component](./#the-component-object) instances.&#x20;

```javascript
...
let digitalRiverCheckout;
let components;
...
digitalRiverCheckout = new DigitalRiverCheckout(publicApiKey);
components = digitalRiverCheckout.components(configurationOptions);
...
```

#### The components configuration object

Refer to [Configuring components](configuring-components.md)

## The components object

A components, which exposes [`createComponent()`](./#createcomponent-componenttype), manages a group of individual [component](./#the-component-object) instances.

### `createComponent(componentType)`

The `createComponent()` function, which requires passing a [supported type](./#supported-component-types), creates an individual [component](./#the-component-object).

```javascript
let paymentComponent;
...
components = digitalRiverCheckout.components(configurationOptions);
paymentComponent = components.createComponent('payment');
```

#### Supported component types

* [`'address'`](address-component.md)
* [`'shipping'`](shipping-component.md)
* [`'taxidentifier'`](tax-identifier-component.md)
* [`'invoiceattribute'`](invoice-component.md)
* [`'wallet'`](wallet-component.md)
* [`'payment'`](payment-component.md)
* [`'compliance'`](compliance-component.md)
* [`'ordersummary'`](order-summary-component.md)
* [`'thankyou'`](thank-you-component.md)

## The component object

The individual component object, which exposes [`mount()`](./#mount-elementid) and, in some cases, [`done()`](./#done), allows you to collect information from and present information to customers.

### `mount(elementId)`

The `mount()` function, which requires that you pass the `id` of an HTML element, attaches that [component](./#the-component-object) to your [DOM](https://en.wikipedia.org/wiki/Document\_Object\_Model).&#x20;

```javascript
<div id="payment-container" style="display: block">
...
paymentComponent.mount('payment-container');
...
```

### `done()`

The [address component](address-component.md), [tax identifier component](tax-identifier-component.md), [shipping component](shipping-component.md), and [invoice component](invoice-component.md) expose `done()`, which submits a customer's data and returns a boolean indicating whether it's valid. For details refer to:

* [Submitting the address component](address-component.md#submitting-the-address-component)
* [Submitting the tax identifier component](tax-identifier-component.md#submitting-the-tax-identifier-component)
* [Submitting the shipping component](shipping-component.md#submitting-the-shipping-component)
* [Submitting the invoice component](invoice-component.md#submitting-the-invoice-component)



