---
description: >-
  Gain a better understanding of how to set up local pricing for use in low-code
  checkouts
---

# Offering local pricing

If you'd like to pair one of Digital River's [low-code checkout options](./) with [local pricing](../../using-our-services/local-pricing.md), this page contains information on:

* [Setting up the shopping experience](offering-local-pricing.md#setting-up-the-shopping-experience)
* [How product prices are displayed throughout the shopping experience](offering-local-pricing.md#product-prices-during-the-shopping-experience)
* [Accessing price formatting rules](offering-local-pricing.md#access-price-formatting-rules)

With both [Prebuilt Checkout](drop-in-checkout.md) and [Components](implementing-a-components-checkout.md), the local pricing functionality exists within [DigitalRiverCheckout.js](../../developer-resources/digitalrivercheckout.js-reference/).

## Setting up the shopping experience

When building your shopping experience, one possible solution is to wait until the document loads and then, at a minimum, define [`containerId`](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md#containerid). Digital River needs this value to determine where to display the [local pricing selector](../../using-our-services/local-pricing.md#local-pricing-selector). Although it's not a hard requirement, you should also populate [`priceElement`](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md#priceelement) so we know which of your [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model/Introduction) elements contain product prices.&#x20;

You also have the option to define how you want to handle various [selector events](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md#local-pricing-selector-events). These events can be useful for testing, analytics, and triggering redirections. For example, you might handle [`onSave`](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md#onsave) by checking the value of `country`, and then, if it's `US` or `CA`, redirect to an experience or store that's customized for shoppers in those countries.

```javascript
document.addEventListener('DOMContentLoaded', () => {
  const config = {
    countrySelector: {
      containerId: 'country-selector',
      priceElement: ['div.price', 'span.price'],
      autoOpen: true,
      onReady: () => {},
      onOpen: () => {},
      onSelect: (data) => {},
      onSave: (data) => {},
      onCancel: () => {}
    }
  };
  ...
```

You can then use this [configuration object](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/digitalrivercheckout-configuration-object.md) to [initialize DigitalRiverCheckout.js](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/).

How you set up the rest of the experience depends on whether you're using [Prebuilt Checkout](offering-local-pricing.md#local-pricing-with-prebuilt-checkout) or [Components](offering-local-pricing.md#local-pricing-with-components).

```javascript
  ...
  const digitalRiverCheckout = new DigitalRiverCheckout('Your public API key', config);
  ...
```

### Local pricing with Prebuilt Checkout

If you want Digital River to create a checkout button, call [`renderButton()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/).&#x20;

<pre class="language-javascript"><code class="lang-javascript"><strong>  ...
</strong><strong>  digitalRiverCheckout.renderButton(buttonContainer, buttonOptions);
</strong><strong>  ...
</strong></code></pre>

The function's [first parameter](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#button-container) is the `id` of the element where you want the button to display.

```javascript
 <div id="button-container"></div>
 ...
 const buttonContainer = '#button-container';
 ...
```

The [second parameter](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#button-options) is a configuration object that, among other things, allows you to (1) [style the button](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#style-the-button), (2) [modify its text](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#customize-the-buttons-text), and (3) [hide your elements](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#hide-elements).

```javascript
  ...
  const buttonOptions = {
    style: {
      backgroundColor: '#B52',
      borderRadius: '100px',
      color: '#5C6',
      fontSize: '2rem',
      fontWeight: '800',
      fontFamily: 'Montserrat,Arial,Helvetica,sans-serif',
      ':hover': {
        color: 'rgb(0, 167, 225)'
      }
    },
    buttonText: 'Proceed to checkout',
    hiddenElement: ['#checkout-btn'],
    afterRender: true,
    onInit: (actions) => {
      console.log('The button has rendered');
    },
    ...
    onCancel: () => {
      console.log('The checkout window has been closed');
    }
  };
  ...
});
```

This object also contains an [`onClick`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/#button-click-event) property you can assign an [`async`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function) event-handling procedure. One way to define it is by using a [`try...catch`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) block that first calls [`actions.loading.start()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/performing-actions-on-the-checkout-button.md#start-and-stop-a-loading-spinner) and then your own create checkout-session function. Make sure to use [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) with this expression so that the handler pauses until a [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise) is returned.

```javascript
  ...
  const buttonOptions = {
    ...
    onClick: async (actions) => {
      console.log('The button has been clicked');
      try {
        actions.loading.start();
        const checkoutSessionId = await createCheckoutSession();
        actions.loading.stop();
        if (!checkoutSessionId) {
          return;
        }
        const config = getConfigObj();
        actions.checkout.modal.open(checkoutSessionId, config);
      } catch (error) {
        actions.loading.stop();
      }
    },
    ...
  };
  ...
});
```

On your front-end, in `onClick`, call [`actions.loading.stop()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/performing-actions-on-the-checkout-button.md#start-and-stop-a-loading-spinner) and then check the value of the promise. If it's [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy), your procedure should reject it and halt execution. Otherwise, pass the returned identifier and, optionally, a [configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/) to [`actions.checkout.modal.open()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/rendering-a-checkout-button/performing-actions-on-the-checkout-button.md#open-a-checkout-modal).

### Local pricing with Components

### Configuring the checkout-session for local pricing

When defining the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md):

* Call [`digitalRiver.getCountry()`](../../developer-resources/digitalrivercheckout.js-reference/accessing-country-and-currency.md#digitalriverpricing.getcountry) and [`digitalRiver.getCurrency()`](../../developer-resources/digitalrivercheckout.js-reference/accessing-country-and-currency.md#digitalriverpricing.getcurrency) and then assign the returned values to the [`shoppingCountry`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#shopping-country) and [`currency`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#currency) parameters, respectively.
* For each product in the customer's cart, retrieve its original, unconverted price and assign it to [`items[].price`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data).
* If you're discounting an entire transaction or individual line items within that transaction, use `discount.percentOff` or `items[].discount.percentOff`. In both cases, don't define `amountOff`.

In your server-side `POST` to [`/drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), make sure to send your [secret API key](../../developer-resources/api-structure.md#confidential-keys).&#x20;

## Product prices during the shopping experience

In both [low-code checkout options](./), Digital River uses the [checkout-session's](../../developer-resources/digital-river-api-reference/checkout-sessions.md) `shoppingCountry`, `currency`, and `items[].price` to perform another currency conversion and then applies the same [rounding](../../using-our-services/local-pricing.md#rounding-logic) and [formatting](offering-local-pricing.md#access-price-formatting-rules) rules used to display prices on your site. As a result, the currency-denominated prices customers see on your storefront and in your cart are identical to those in the checkout experience.&#x20;

{% tabs %}
{% tab title="Storefront " %}
<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Cart" %}
<figure><img src="../../.gitbook/assets/image (110).png" alt="" width="375"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Components" %}
<figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Access price formatting rules

Once customers provide payment, complete their purchase, and Digital River converts the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), we add `pricingFormat` to the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).

{% code title="checkout_session.order.created" %}
```json
{
    "id": "dacc88d7-3f88-469b-9764-35a15681e6c9",
    ...
            "pricingFormat": {
                "currencyNumberFormat": "#,###.##",
                "symbol": "₩",
                "decimalPlaces": 0,
                "currencySymbolBeforePrice": true,
                "useCurrencySymbolSpace": false
            },
            "liveMode": false
        }
    },
    ...
}
```
{% endcode %}

This object contains the rules Digital River used to format prices throughout the [shopping experience](offering-local-pricing.md#product-prices-during-the-shopping-experience). To maintain a consistent format, you can apply these rules to the prices in your [customer notifications](../../order-management/customer-notifications.md) and your site's order management pages.

{% hint style="info" %}
Both [`onCheckoutComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#oncheckoutcomplete) and [`onSuccess`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#success-event) also return `pricingFormat`. &#x20;
{% endhint %}

```json
{
    "id": "764ddbdd-0f7e-448d-b044-196f67dd1781",
    "type": "checkout_session.order.created",
    "data": {
        "object": {
            ...
            "pricingFormat": {
                "currencyNumberFormat": "#,###.##",
                "symbol": "¥",
                "decimalPlaces": 0,
                "currencySymbolBeforePrice": true,
                "useCurrencySymbolSpace": false
            },
            ...
        }
    },
    ...
}
```

{% hint style="success" %}
If you don't want to build your formatter, many server-side languages have pre-built functions that roughly approximate the formatter Digital River uses. Depending on your application, you might find some of the following pages useful:

* [Java: Numbers and currencies](https://docs.oracle.com/javase/tutorial/i18n/format/numberintro.html)
* [PHP: Number and currency formatter](https://www.php.net/manual/en/numberformatter.formatcurrency.php)
* [Python: Internationalization services](https://rubymoney.github.io/money/)
* [Ruby: Money](https://rubymoney.github.io/money/)
{% endhint %}

The following objects are nested in `pricingFormat`:

* [`currencyNumberFormat`](offering-local-pricing.md#currencynumberformat)
* [`symbol`](offering-local-pricing.md#symbol)
* [`decimalPlaces`](offering-local-pricing.md#decimalplaces)
* [`currencySymbolBeforePrice`](offering-local-pricing.md#currencynumberformat)
* [`useCurrencySymbolSpace`](offering-local-pricing.md#usecurrencysymbolspace)

#### &#x20;`currencyNumberFormat`&#x20;

You can use `currencyNumberFormat` to determine how to display the integer and fractional parts of a price.&#x20;

Its value indicates whether the character that groups digits in the integer part should be a comma (`,`), a point (`.`), an apostrophe (`'`), a whitespace( ), or some other character. It also dictates the correct spacing of this character.&#x20;

Additionally, `currencyNumberFormat` allows you to determine whether the character that separates the price's integer part from its fractional part should be a point or a comma.

{% tabs %}
{% tab title="Example 1" %}
In the following example, `currencyNumberFormat` indicates that the digits in the integer part should be grouped by a comma placed every third digit to the left of a point, which acts as the separator between the price's integer and fractional parts.

```json
"currencyNumberFormat": "#,###.##"
```

#### Target output in UI

![](<../../.gitbook/assets/image (48).png>)
{% endtab %}

{% tab title="Example 2" %}
In the following example, `currencyNumberFormat` indicates that the digits in the integer part should be grouped by a point that's placed every third digit to the left of a comma, which acts as the separator between the price's integer and fractional parts.

```json
"currencyNumberFormat": "#.###,##"
```

#### Target output in UI

![](<../../.gitbook/assets/image (20).png>)
{% endtab %}

{% tab title="Example 3" %}
In the following example, `currencyNumberFormat` indicates that the digits in the integer part should first be grouped by a comma that's placed every third digit to the left of a point, which acts as the separator between the price's integer and fractional parts.&#x20;

After that, digits in the integer part should follow a two-digit grouping pattern.&#x20;

```json
"currencyNumberFormat": "#,##,###.##"
```

#### Target output in UI

![](<../../.gitbook/assets/image (23).png>)
{% endtab %}

{% tab title="Example 4" %}
In the following example, `currencyNumberFormat` indicates that the digits in the integer part should be grouped by an apostrophe that's placed every third digit to the left of a point, which acts as the separator between the price's integer and fractional parts.

```json
"currencyNumberFormat": "#'###.##"
```

#### Target output in UI

![](<../../.gitbook/assets/image (63).png>)
{% endtab %}
{% endtabs %}

#### `symbol`

The graphic `symbol` that should be used to denote the price's currency.

{% tabs %}
{% tab title="Example 1" %}
The following is the `symbol` for Swiss Francs:

```json
"symbol": "CHF"
```

#### Target output in UI

![](<../../.gitbook/assets/image (97).png>)
{% endtab %}

{% tab title="Example 2" %}
The following is the `symbol` for Jordanian Dinars:

```json
"symbol": "د.ا"
```

#### Target output in UI

![](<../../.gitbook/assets/image (17) (1).png>)
{% endtab %}
{% endtabs %}

#### `decimalPlaces`

This stipulates the number of digits that should be displayed to the right of the character (whether it's a point or comma) that divides a price's integer part from its fractional part.

If `decimalPlaces` is `0` and [`currencyNumberFormat`](offering-local-pricing.md#currencynumberformat) indicates that a character should be placed between the integer and fractional parts, then that character shouldn't be displayed.

```json
{
    ...
    "pricingFormat": {
        "currencyNumberFormat": "#,###.##",
        ...
        "decimalPlaces": 0,
        ...
    },
    ...
}
```

| decimalPlaces value | Target output in UI                                                          |
| ------------------- | ---------------------------------------------------------------------------- |
| `0`                 | ![](<../../.gitbook/assets/image (18) (1).png>)                              |
| `2`                 | <img src="../../.gitbook/assets/image (89).png" alt="" data-size="original"> |
| `3`                 | ![](<../../.gitbook/assets/image (21).png>)                                  |

#### `currencySymbolBeforePrice`

The `currencySymbolBeforePrice` indicates whether [`symbol`](offering-local-pricing.md#symbol) should be placed before or after a price's numeric amount.

<table><thead><tr><th width="324.3333333333333">currencySymbolBeforePrice value</th><th>Target output in UI</th></tr></thead><tbody><tr><td><code>true</code></td><td><img src="../../.gitbook/assets/image (94).png" alt=""></td></tr><tr><td><code>false</code></td><td><img src="../../.gitbook/assets/image (26).png" alt=""></td></tr></tbody></table>



#### `useCurrencySymbolSpace`

The `useCurrencySymbolSpace` indicates whether or not to insert a space between [`symbol`](offering-local-pricing.md#symbol) and the price's numeric amount.

| useCurrencySymbolSpace value | Target output in UI                         |
| ---------------------------- | ------------------------------------------- |
| `true`                       | ![](<../../.gitbook/assets/image (51).png>) |
| `false`                      | ![](<../../.gitbook/assets/image (31).png>) |
