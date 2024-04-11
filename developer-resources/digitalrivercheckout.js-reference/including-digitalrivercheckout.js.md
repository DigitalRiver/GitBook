---
description: Learn how to load DigitalRiverCheckout.js on your checkout page
---

# Including DigitalRiverCheckout.js

To leverage the functionality included in DigitalRiverCheckout.js, add a [`script`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) with a `src` attribute that specifies the library's location.

```html
<script defer="defer" src="https://checkout.digitalriverws.com/v1/DigitalRiverCheckout.js"></script>
```

We recommend loading DigitalRiverCheckout.js using the `async` or `defer` attribute. This won't block DOM rendering during [script loading](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First\_steps/What\_is\_JavaScript#script\_loading\_strategies) and, as result, can improve your site's user experience. However, with asynchronous loading, make sure you don't make any API calls until after the script finishes executing.&#x20;
