---
description: Reference documentation for the DynamicPricing.js library
---

# DynamicPricing.js reference

This page documents the scripts, element attributes and functions available in Digital River's browser-side DynamicPricing.js library.

## Local pricing script <a href="#dynamic-pricing-script" id="dynamic-pricing-script"></a>

On each `html` page that contains [price elements](dynamicpricing.js-reference.md#price-elements), you must have a `script` with an `id` of `DR-Dynamic-Pricing`.

With the exception of the [script's attributes](dynamicpricing.js-reference.md#script-attributes), the following code must remain unaltered:

```html
<script id="DR-Dynamic-Pricing">
        (function () {
            var s = document.createElement('script');
            s.type = 'text/javascript';
            s.async = true;
            s.setAttribute('data-dr-apiKey', 'YOUR_PUBLIC_API_KEY')
            // optional - defaults to 'DR-currencySelector'
            s.setAttribute('data-dr-currency-selector', 'currency-selector');
            // optional - defaults to browser language
            s.setAttribute('data-dr-default-country', 'FR');
            s.src = 'https://js.digitalriver.com/v1/DynamicPricing.js';
            document.getElementsByTagName('head')[0].appendChild(s);
        })();
    </script>

```

### Script attributes

In the [local pricing script](dynamicpricing.js-reference.md#dynamic-pricing-script), the following attributes are configurable:

* [`data-dr-apiKey`](dynamicpricing.js-reference.md#data-dr-apikey)
* [`data-dr-currency-selector`](dynamicpricing.js-reference.md#data-dr-currency-selector)
* [`data-dr-default-country`](dynamicpricing.js-reference.md#data-dr-default-country)

#### `data-dr-apiKey`

You're required to set `data-dr-apiKey` and the value you pass must be your [public API key](api-structure.md#public-keys).

#### `data-dr-currency-selector`

You can optionally set `data-dr-currency-selector`. If you do, a DOM element whose `id` is the same value as `data-dr-currency-selector` needs to be on the page.&#x20;

The default value is `DR-currencySelector`.

For more details, refer to [Specify a local pricing selector element](dynamicpricing.js-reference.md#specify-a-dynamic-pricing-selector-element).&#x20;

#### `data-dr-default-country`

You can use the optional `data-dr-default-country` attribute to help determine which country is selected by default when a page loads. By extension, this also determines the selected currency.

The value you pass must be a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.

When the page loads and the [local pricing script](dynamicpricing.js-reference.md#dynamic-pricing-script) executes, it first looks for the user's country in cookies, next in `data-dr-default-country`, and then in the browser's default language settings. If those searches aren't successful, your account's [base country](../using-our-services/local-pricing.md#base-country-and-currency) is used.

Once a value is located, DynamicPricing.js makes a call to determine that country's default currency. The [local pricing selector's](dynamicpricing.js-reference.md#dynamic-pricing-selector) drop-down menus then display these country and currency values. Additionally, your [price elements](dynamicpricing.js-reference.md#price-elements) are denoted in this currency.&#x20;

## Local pricing selector <a href="#dynamic-pricing-selector" id="dynamic-pricing-selector"></a>

The [local pricing selector](../using-our-services/local-pricing.md#local-pricing-selector) allows customers to select a country-currency combination while shopping on your site.

To configure it, you'll need to (1) [designate a DOM element](dynamicpricing.js-reference.md#specify-a-dynamic-pricing-selector-element) and (2) [apply a stylesheet](dynamicpricing.js-reference.md#style-the-dynamic-pricing-selector).

#### Specify a local pricing selector element <a href="#specify-a-dynamic-pricing-selector-element" id="specify-a-dynamic-pricing-selector-element"></a>

You need to include a DOM element that renders the [local pricing selector](dynamicpricing.js-reference.md#dynamic-pricing-selector). The element can be added to header, footer, body, and other HTML tags.

The element's `id` must be (1) `DR-currencySelector` or (2) the value you assign [`data-dr-currency-selector`](dynamicpricing.js-reference.md#data-dr-currency-selector).

{% tabs %}
{% tab title="Default" %}
If you don't set [`data-dr-currency-selector`](dynamicpricing.js-reference.md#data-dr-currency-selector), then `id` of the selector element must be `DR-currencySelector`

```html
<div id="DR-currencySelector">
```
{% endtab %}

{% tab title="Custom" %}
If you set [`data-dr-currency-selector`](dynamicpricing.js-reference.md#data-dr-currency-selector), then `id` of the selector element must be that same value.

```html
...
s.setAttribute('data-dr-currency-selector', 'currency-selector');
...
<div id="currency-selector">
```
{% endtab %}
{% endtabs %}

#### Style the local pricing selector <a href="#style-the-dynamic-pricing-selector" id="style-the-dynamic-pricing-selector"></a>

To style the [local pricing selector](dynamicpricing.js-reference.md#dynamic-pricing-selector), add the following `link`.

```html
<link href="https://js-test.digitalriver.com/v1/css/DynamicPricing.css" rel="stylesheet"/>
```

Alternatively, you can override this stylesheet with your own.&#x20;

## Price elements

Each DOM element on your site that displays pricing information must have a `data-dr-original-price` attribute. These represent your base prices. Make sure the values you pass don't contain a currency symbol or any whitespaces.

```html
<div data-dr-original-price="199.99"></div> 
```

When populating your `data-dr-original-price` attributes, retrieve data from a price list that is associated with your account's [base country and base currency](../using-our-services/local-pricing.md#base-country-and-currency).&#x20;

{% hint style="info" %}
To retrieve your base country and currency, pass your [public API key](api-structure.md#public-keys) in the header of a `GET /dynamic-pricing/country-currency` request.&#x20;
{% endhint %}

Also, depending on [your account's tax configurations](../using-our-services/local-pricing.md#taxes), make sure that your `data-dr-original-price` values are either tax inclusive or tax exclusive. For details, contact your Digital River representative.&#x20;

When the [local pricing script](dynamicpricing.js-reference.md#dynamic-pricing-script) executes or customers modify currency and/or country in the [selector](dynamicpricing.js-reference.md#dynamic-pricing-selector), DynamicPricing.js makes a call to get country-currency specific data, and then checks whether the country is both supported by Digital River and setup to allow [variable pricing](../using-our-services/local-pricing.md#fixed-prices). If these conditions are met, DynamicPricing.js applies a conversion factor and a [rounding function](../using-our-services/local-pricing.md#rounding-logic) to each `data-dr-original-price` on the page, implements [currency formatting rules](../integration-options/low-code-checkouts/drop-in-checkout.md#pricing-format) and then displays the converted, formatted value in the DOM element's `innerHTML` and adds `data-dr-converted-price` and `data-dr-formatted-price` to the element's attributes.

{% code overflow="wrap" %}
```html
<div class="price" data-dr-original-price="199" data-dr-currency="EUR" data-dr-country="FR" data-dr-converted-price="230.00" data-dr-formatted-price="230,00 €">230,00 €</div>
```
{% endcode %}

## Getting country and currency

The [local pricing script](dynamicpricing.js-reference.md#dynamic-pricing-script) creates the `digitalRiverPricing` object which exposes [`getCountry(`](dynamicpricing.js-reference.md#digitalriverpricing.getcountry)`)` and [`getCurrency()`](dynamicpricing.js-reference.md#digitalriverpricing.getcurrency).&#x20;

### `digitalRiverPricing.getCountry()`

Call `digitalRiverPricing.getCountry(`) to get the country that is selected in the[ local pricing selector](dynamicpricing.js-reference.md#dynamic-pricing-selector).&#x20;

```javascript
digitalRiverPricing.getCountry();
```

The returned value is formatted as an [Alpha-2 country code](https://www.iban.com/country-codes).&#x20;

### `digitalRiverPricing.getCurrency()`

Call `digitalRiverPricing.getCurrency()` to get the currency that is selected in the [local pricing selector](dynamicpricing.js-reference.md#dynamic-pricing-selector).

```javascript
digitalRiverPricing.getCountry()
```

The returned value is formatted as a three-letter alphabetic code that conforms to the [ISO 4217](https://www.xe.com/iso4217.php) standard.
