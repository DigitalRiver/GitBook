---
description: >-
  Learn about the functionality that exists within the DigitalRiverCheckout
  configuration object
---

# DigitalRiverCheckout configuration object

The [initialize DigitalRiverCheckout.js function](./) accepts an optional configuration object, which allows you to [define a local pricing selector](digitalrivercheckout-configuration-object.md#defining-a-local-pricing-selector).

## Defining a local pricing selector

If you [pair the local pricing service with a low-code checkout](../../../integration-options/low-code-checkouts/offering-local-pricing.md), you'll need to define [`countrySelector`](digitalrivercheckout-configuration-object.md#countryselector).

<pre class="language-javascript" data-full-width="false"><code class="lang-javascript"><strong>const config = {
</strong>  countrySelector: {
    containerId: 'country-selector',
    priceElement: ['div.price', 'span.price'],
    onReady: () => {},
    onOpen: () => {},
    onSelect: (data) => {},
    onSave: (data) => {},
    onCancel: () => {}
  }
};  
...
const digitalRiverCheckout = new DigitalRiverCheckout('YOUR_PUBLIC_API_KEY', config);
</code></pre>

### `countrySelector`

The `countrySelector` object allows you to:

* [Specify a container for the local pricing selector.](digitalrivercheckout-configuration-object.md#containerid)
* [Inform Digital River which of your product prices to convert.](digitalrivercheckout-configuration-object.md#priceelement)&#x20;
* [Listen for and handle selector callback events.](digitalrivercheckout-configuration-object.md#local-pricing-selector-events)

#### `containerId`

The required `containerId` represents the `id` of an [HTML element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) in which [DigitalRiverCheckout.js](../) should render the [local pricing selector](../../../using-our-services/local-pricing.md#local-pricing-selector).

```javascript
const config = {
  countrySelector: {
    containerId: 'country-selector',
    ...
  }
};  
```

#### `priceElement`

The optional `priceElement` represents an array of [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_Selectors) strings that [DigitalRiverCheckout.js](../) uses to target each element on your page that displays pricing information.

For example, `span.price` in the following `priceElement` targets all `<span>` elements that have a `class` attribute of `"price"`.

```javascript
const config = {
  countrySelector: {
    ...
    priceElement: ['div.price', 'span.price'],
    ...
  }
};  
```

When users modify currency or country in the [selector](../../../using-our-services/local-pricing.md#local-pricing-selector), we make a call to determine whether Digital River supports that country and it's set up for [variable pricing](../../../using-our-services/local-pricing.md#fixed-prices). If this is the case, for each `priceElement`, we apply a conversion factor and a [rounding function](../../../using-our-services/local-pricing.md#rounding-logic), implement currency formatting rules, display a converted, formatted value in its `innerHTML` and add selected currency, selected country, converted price, formatted price, and original price attributes.

```html

<span class="price" data-dr-original-price="299" data-dr-currency="INR" data-dr-country="IN" data-dr-converted-price="25000.00" data-dr-formatted-price="₹25,000.00">₹25,000.00</span>
```

### Local pricing selector events

In [`countrySelector`](digitalrivercheckout-configuration-object.md#countryselector), you can assign callback methods to [`onReady`](digitalrivercheckout-configuration-object.md#onready), [`onOpen`](digitalrivercheckout-configuration-object.md#onopen), [`onSelect`](digitalrivercheckout-configuration-object.md#onselect), [`onSave`](digitalrivercheckout-configuration-object.md#onsave), and [`onCancel`](digitalrivercheckout-configuration-object.md#oncancel), which allow you to listen for various [local pricing selector](../../../using-our-services/local-pricing.md#local-pricing-selector) events and then define how you want to handle them.&#x20;

```javascript
const config = {
  countrySelector: {
    ...
    onReady: () => {},
    onOpen: () => {},
    onSelect: (data) => {},
    onSave: (data) => {},
    onCancel: () => {}
  }
};  
```

#### `onReady`

The optional `onReady` property can be assigned a callback method that executes when the [local pricing selector](../../../using-our-services/local-pricing.md#local-pricing-selector) is ready to accept user input.&#x20;

{% hint style="info" %}
When it executes, [`digitalRiverPricing`](../accessing-country-and-currency.md#digitalriverpricing) has been defined. For details, refer to [Accessing country and currency](../accessing-country-and-currency.md).&#x20;
{% endhint %}

```javascript
const config = {
  countrySelector: {
    ...
    onReady: () => {
      console.log('The country-currency selector is ready to accept input');
    },
    ...
  }
};
```

#### `onOpen`

The optional `onOpen` property can be assigned a callback method that executes when the user clicks on the country-currency icon and the [local pricing selector](../../../using-our-services/local-pricing.md#local-pricing-selector) opens.

```javascript
const config = {
  countrySelector: {
    ...
    onOpen: () => {
      console.log('The user opened the country-currency selector');
    },
    ...
  }
};
```

#### `onSelect`

The optional `onSelect` property can be assigned a callback method, which accepts `data`, that executes when the user makes a selection in the [local pricing selector](../../../using-our-services/local-pricing.md#local-pricing-selector). In `data`, the method returns either `country` or `currency`, depending on which the user selected.&#x20;

```javascript
const config = {
  countrySelector: {
    ...
    onSelect: (data) => {
      if (data.hasOwnProperty('country')) {
        console.log('The user selected the country of ' + data.country)
      } else {
        console.log('The user selected a currency of ' + data.currency);
      }
    },
    ...
  }
};
```

#### `onSave`

The optional `onSave` property can be assigned a callback method, which accepts `data`, that executes when the user clicks the [local pricing selector's](../../../using-our-services/local-pricing.md#local-pricing-selector) save button. In `data`, the method returns the `country` and `currency` that the user saved.

```javascript
const config = {
  countrySelector: {
    ...
    onSave: (data) => {
      console.log('The user clicked the save button. The saved country and currency is ' + data.country + ' and ' + data.currency + ", respectively");
    },
    ...
  }
};
```

#### `onCancel`

The optional `onCancel` property can be assigned a callback method that executes when the user clicks the [local pricing selector's](../../../using-our-services/local-pricing.md#local-pricing-selector) cancel button.

```javascript
const config = {
  countrySelector: {
    ...
    onCancel: () => {
      console.log('The user clicked the cancel button');
    }
  }
};
```
