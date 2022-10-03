---
description: Understand how to use locale and currency.
---

# Locale and currency

A locale is a designator that combines the two-letter [ISO 639-1](https://en.wikipedia.org/wiki/ISO\_639-1) language code with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code (for example, en-US). When you set up your store in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), you specified a default locale. Your store automatically shows the language and currency of the default locale.

The currency is a designatory that uses a [three-letter currency code](https://www.iban.com/currency-codes) to identify the currency.

When creating a shopper through Commerce API, the default locale and currency can be specified in the request body; if the locale and currency are not provided, then it will use the default locale and currency for this shopper.

When creating a shopper through Commerce API, the default locale and currency can be specified in the request body; if the locale and currency are not provided, then it will use the default locale and currency for this shopper.

{% code overflow="wrap" %}
```javascript
{
  "shopper": {
    "username": "jswanson@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jswanson@digitalriver.com",
    "password": "qwerasdf",
    "locale": "en_CH",
    "currency": "CHF",
    "sendMail": true,
    "sendEMail": true
  }
}
```
{% endcode %}

After the shopper adds a product to create a shopping cart, the locale and currency of the shopping cart will be the default for the current shopper's cart.

The shopper can update their default locale and currency for their current shopping cart by using the `/shoppers/me` endpoint.
