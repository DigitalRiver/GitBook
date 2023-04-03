---
description: Learn how to use the Digital River publishable API key.
---

# Digital River publishable API key

Use the `DigitalRiver(publishableAPIKey)` object to create an instance of the DigitalRiver object. This is called a Digital River publishable API key.

{% code overflow="wrap" %}
```javascript
let digitalriver = new DigitalRiver("YOUR_PUBLIC_API_KEY", {
     "locale": "en-us"
});
```
{% endcode %}

This function accepts an optional `options` object using the following format: `DigitalRiver(publishableApiKey[, options])`

You may specify the following options within this object.

| Option | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| locale | <p>The locale used to localize the various display and error strings within DigitalRiver.js</p><p>Currently supported locales:</p><p>ar-EG, cs-CZ, da-DK, de-AT, de-CH, de-DE, el-GR, en-AU, en-CA, en-GB, en-IE, en-IN, en-NZ, en-PR, en-US, en-ZA, es-AR, es-CL, es-CO, es-EC, es-ES, es-MX, es-PE, es-VE, et-EE, fi-FI, fr-BE, fr-CA, fr-CH, fr-FR, hu-HU, it-CH, it-IT, iw-IL, ja-JP, ko-KR, nl-BE, nl-NL, no-NO, pl-PL, pt-BR, pt-PT, ro-RO, ru-RU, sv-SE, th-TH, tr-TR, zh-CN, zh-HK, zh-TW</p> |

## Localizing DigitalRiver.js

‌The following example localizes the various display and error strings to English (United States).

{% code overflow="wrap" %}
```
let digitalriver = new DigitalRiver("YOUR_PUBLIC_API_KEY", {     "locale": "en-us"});
```
{% endcode %}

‌
