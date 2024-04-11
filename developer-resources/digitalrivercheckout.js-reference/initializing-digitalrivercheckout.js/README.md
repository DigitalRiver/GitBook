---
description: >-
  Learn how to use your public API key and an optional configuration object to
  create an instance of DigitalRiverCheckout
---

# Initializing DigitalRiverCheckout.js

Use `DigitalRiverCheckout()` with the [`new`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) operator to construct an instance of the [`DigitalRiverCheckout` object](../digitalrivercheckout-object/). This function accepts a required [public API key](../../api-structure.md#api-keys) and an optional [configuration object](digitalrivercheckout-configuration-object.md).

```javascript
const digitalRiverCheckout = new DigitalRiverCheckout('YOUR_PUBLIC_API_KEY', config);
```
