---
description: >-
  Gain a better understanding of the local pricing service, its benefits, and
  your configuration options
---

# Local pricing

With local pricing, you can build a storefront and checkout experience that allows customers to select their shopping country and the currency in which they want to conduct a transaction and then be presented with converted prices.&#x20;

<figure><img src="../.gitbook/assets/dynamic pricing.png" alt=""><figcaption></figcaption></figure>

On this page, you'll find information on:

* [The benefits of the local pricing service](local-pricing.md#benefits-of-the-service)
* [How your account can be set up to use it](local-pricing.md#setting-up-your-account)

For details on pairing one of our [low-code checkout options](../integration-options/low-code-checkouts/) with local pricing, refer to [Offering local pricing](../integration-options/low-code-checkouts/offering-local-pricing.md).

## Benefits of the service

Digital River's local pricing service:

* Allows you to maintain a single price list in a fixed currency, assign that data to elements in your [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model), and then make sales in multiple countries and currencies. &#x20;
* Allows customers to [select various country-currency combinations](local-pricing.md#local-pricing-selector) while shopping on your site and then be presented with converted prices.&#x20;
* Maintains consistency between the prices customers see on your storefront, in your cart, and in the checkout.
* Employs [rounding logic](local-pricing.md#rounding-logic) to make your prices more consumer friendly.
* Uses [standardized rules to format a price's numeric amount and currency](../integration-options/low-code-checkouts/drop-in-checkout.md#pricing-format).
* Gives you the ability to apply [country-specific tax rates](local-pricing.md#taxes) to your storefront prices.&#x20;
* Allows you to maintain [fixed price lists](local-pricing.md#fixed-prices) for designated countries.
* Uses frequently updated exchange rates.

## Setting up your account

Before deployment, you'll need to:

* [Specify a base country and currency](local-pricing.md#base-country-and-currency)
* [Provide a list of countries and currencies you want to support](local-pricing.md#supported-countries-and-currencies)

You also can:

* [Configure taxes](local-pricing.md#taxes)
* [Set fixed prices](local-pricing.md#fixed-prices)
* [Select rounding rules](local-pricing.md#rounding-logic)

Digital River then stores this data in your account, making it available to the local pricing service at run-time.&#x20;

### Base country and currency

Your local pricing account needs to be assigned a base country and currency.&#x20;

{% hint style="info" %}
The original prices you assign to elements in your [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model) should be retrieved from a list associated with this base country-currency pair. &#x20;
{% endhint %}

The values you designate are typically dependent on your trading patterns. For example, if most of your site's customers are in Italy, you'd likely want your base country to be Italy and your base currency to be the euro.&#x20;

Each time Digital River performs a currency conversion, your original prices are converted from your designated base currency to the target currency selected by the customer.&#x20;

Your base country may also affect how prices are displayed when your storefront loads. For details, refer to [`data-dr-default-country`](../developer-resources/dynamicpricing.js-reference.md#data-dr-default-country).

{% hint style="info" %}
The `data-dr-default-country` attribute is only exposed if you're using the [DynamicPricing.js](../developer-resources/dynamicpricing.js-reference.md) library.
{% endhint %}

### Supported countries and currencies

Before deploying, indicate which countries and currencies you want to support.

The [local pricing selector](local-pricing.md#local-pricing-selector) allows customers to choose from your designated currencies. Alternatively, your account can be configured so customers shopping in a specific country are always restricted to using a single default currency.&#x20;

### Taxes <a href="#taxes" id="taxes"></a>

The local pricing service gives you a variety of ways to configure taxes.

For each of your [supported countries](local-pricing.md#supported-countries-and-currencies), you can specify whether taxes should be included in your storefront prices.&#x20;

{% hint style="info" %}
Customers in EU nations typically expect prices to be displayed with value-added tax (VAT) included, while US customers are accustomed to seeing taxes added at checkout time.&#x20;
{% endhint %}

Suppose the values in your [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model) price elements are tax exclusive, and a requirement exists in the customer's selected country that storefront prices include taxes. In that case, you can configure the service to add the appropriate tax amount to your price values.&#x20;

Alternatively, if assign tax-inclusive values to your DOM price elements, but no such requirement exists in the customer's country, then the service can extract the tax portion of your prices and only display their product portion.&#x20;

Finally, if your base prices include taxes, and customers select a country you've indicated should display tax-inclusive prices, then the service can subtract taxes from your values and add back the amount applicable to that selected country.

{% hint style="success" %}
Based on your trading patterns, your Digital River representative can help determine your optimal tax setup.
{% endhint %}

You can also set country-specific tax rates or allow each country's default tax rate to be applied to your product prices. &#x20;

### Fixed prices

For each of your [supported countries](local-pricing.md#supported-countries-and-currencies), you can indicate whether you want your product prices to be fixed or variable  If you make them fixed, customers shopping in that country are restricted to using its default currency.

You might find this feature useful if you maintain a static price list for a specific country and don't want it modified by the local pricing service. In this case, the values you assign to your [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model) price elements are what customers see on your storefront and in the [Prebuilt Checkout modal](../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window).&#x20;

### Rounding logic

The local pricing service contains rounding logic that handles the aesthetically unappealing and inconsistent product prices that often result from currency conversions. Exchange rates fluctuate, but these rules help keep your storefront prices stable. For example, rather than presenting a conversion as $124.28, the service might render that price as $123.99 or $125.00.&#x20;

You can configure a unique pretty pricing rule for each of your [supported currencies](local-pricing.md#supported-countries-and-currencies).&#x20;

## Local pricing selector

The local pricing selector allows customers to select a country-currency combination while shopping on your site.

![](<../.gitbook/assets/image (76).png>)

The selector's country drop-down displays all of your [supported countries](local-pricing.md#supported-countries-and-currencies).&#x20;

When customers choose a different country, the selector's currency drop-down defaults to that country's default currency. If you set up your account so that all transactions in the selected country must be conducted in that currency, then only that option is available. Otherwise, all the [currencies saved to your account](local-pricing.md#supported-countries-and-currencies) are presented as options.

## Next steps

For details on pairing one of our [low-code checkout options](../integration-options/low-code-checkouts/) with local pricing, refer to [Offering local pricing](../integration-options/low-code-checkouts/offering-local-pricing.md).
