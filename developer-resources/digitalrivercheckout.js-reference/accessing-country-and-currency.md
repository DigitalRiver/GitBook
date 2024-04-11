---
description: >-
  If you're using local pricing with a low-code checkout solution, learn how to
  access the country and currency selected by customers
---

# Accessing country and currency

If you're using the [local pricing service](../../using-our-services/local-pricing.md) with a [low code checkout solution](../../integration-options/low-code-checkouts/), then [`digitalRiverPricing`](accessing-country-and-currency.md#digitalriverpricing) allows you to access the user's selected country and currency[.](../../using-our-services/local-pricing.md#local-pricing-selector)&#x20;

## `digitalRiverPricing`

The `digitalRiverPricing` object, which you can access after [`onReady`](initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md#onready) executes, exposes [`getCountry()`](accessing-country-and-currency.md#digitalriverpricing.getcountry) and [`getCurrency()`](accessing-country-and-currency.md#digitalriverpricing.getcurrency).

### `digitalRiverPricing.getCountry()`

Call `digitalRiverPricing.getCountry(`) to retrieve the country currently selected in the [local pricing selector](../../using-our-services/local-pricing.md#local-pricing-selector).&#x20;

```javascript
digitalRiverPricing.getCountry();
```

The returned value is formatted as an [Alpha-2 country code](https://www.iban.com/country-codes).&#x20;

### `digitalRiverPricing.getCurrency()`

Call `digitalRiverPricing.getCurrency()` to retrieve the currency that is currently selected in the [local pricing selector](../../using-our-services/local-pricing.md#local-pricing-selector).&#x20;

```javascript
digitalRiverPricing.getCountry()
```

The returned value is formatted as a three-letter alphabetic code that conforms to the [ISO 4217](https://www.xe.com/iso4217.php) standard.
