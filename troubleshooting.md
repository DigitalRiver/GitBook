---
description: Learn how to troubleshoot the WordPress Plugin.
---

# Troubleshooting

## How to avoid PayPal overriding the GlobalCommerce address

To restrict the user from overriding the shipping address via PayPal, in the createSource request, send a value of `false` as the `requestShipping` element.

```
let payPalPayload = {

                        'type': 'payPal',

                        'amount': cart.pricing.orderTotal.value,

                        'currency': 'USD',

                        'payPal': {

                            'returnUrl': window.location.href + '?ppsuccess=true',

                            'cancelUrl': window.location.href + '?ppcancel=true',

                            'items': payPalItems,

                            'taxAmount': cart.pricing.tax.value,

                            'requestShipping':  requestShipping  false
```

## Shoppers are landing on the login page when the expected behavior is that all shoppers check out as a guest

By default, if the shopper is not logged in or hasn't clicked  **Continue as Guest**, they are redirected to the login page. If the expectation is for all shoppers to checkout as a guest add the following snippet to the theme of the site:

```
<script>
document.cookie = 'drgc_guest_flag=true; path=/';
</script>
```

{% hint style="info" %}
**Note**: There is no specific place to insert the script; both `<head>` and  `<body>` will work. Ensure the script exists on all the pages.
{% endhint %}
