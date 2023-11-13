---
description: Learn how to use the Digital River publishable API key.
---

# Initializing DigitalRiver.js

‌Use `DigitalRiver(publishableAPIKey)` to create an instance of the [`DigitalRiver` object](digitalriver-object.md). The function requires a [public API key](broken-reference).&#x20;

{% code overflow="wrap" %}
```javascript
let digitalriver = new DigitalRiver("YOUR_PUBLIC_API_KEY", {
     "locale": "en-us"
});
```
{% endcode %}

It also accepts [`options`](digital-river-publishable-api-key.md#localizing-digitalriver.js) (_optional_) using the following format: `DigitalRiver(publishableApiKey[, options])`

## ‌Localizing DigitalRiver.js

In `options`, you can specify a `locale` to localize the library.

The following example translates the various display and error strings within DigitalRiver.js into Italian ‌by assigning `it` to `locale`.

{% code overflow="wrap" %}
```javascript
let digitalriver = new DigitalRiver("YOUR_PUBLIC_API_KEY", {
     "locale": "it"
});
```
{% endcode %}
