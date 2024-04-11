---
description: >-
  Apple Pay provides a fast and secure shopping experience where consumers can
  quickly and seamlessly checkout with their Apple Touch authentication without
  login details or credentials.
---

# Apple Pay

A fast and secure shopping experience where the consumer can quickly and seamlessly checkout with their Apple Touch authentication without login details or credentials. Digital River will support Apple Pay as a payment method on the payment service and DigitalRiver.js. Apple Pay is currently available to consumers in many countries and is currently supported only on IOS devices (iPhones, Macs, and so on). &#x20;

{% hint style="info" %}
Apple Pay does not support cross-origin iframes. You can choose not to use cross-origin iframes or set the `allow=payment` attribute at the iframe. See [Support Apply Pay in cross-origin iframes with`allow=payment` attribute](https://bugs.webkit.org/show\_bug.cgi?id=226345) for more information.
{% endhint %}

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/applepay.html) (only viewable on Apple devices).

## How to configure&#x20;

To offer Apple Pay on your website, you must validate your domain with Apple before accepting transactions. To complete this validation:

**Step one**: [Download](https://drapi.io/docs/apple-pay/apple-developer-merchantid-domain-association) the `apple-developer-merchantid-domain-association` file.

**Step two**: Save the file to the following location on the domain where you want to offer Apple Pay: `/.well-known/apple-developer-merchantid-domain-association` \
\
Repeat this step for each additional domain you want to offer Apple Pay. For example:\
`https://buy.mydomain.com/.well-known/apple-developer-merchantid-domain-association`\
`https://shop.mydomain.com/.well-known/apple-developer-merchantid-domain-association`\
`https://www.mydomain.com/.well-known/apple-developer-merchantid-domain-association` \


{% hint style="warning" %}
The URL you specify must be public and globally accessible so that Digital River can complete its verification process.&#x20;

Additionally, you'll need to serve the `apple-developer-merchantid-domain-association` file over HTTPS.
{% endhint %}

**Step three**: Contact your Digital River representative with the list of domains you want to register.

After completing these steps, the remainder of the Apple Pay configuration process depends on whether you use [DigitalRiver.js with Elements](../payment-integrations-1/digitalriver.js/) or [Drop-in payments](../payment-integrations-1/drop-in/).

| DigitalRiver.js with Elements                                                                                                             | Drop-in payments                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [Configuring Apple Pay](../payment-integrations-1/digitalriver.js/payment-methods/apple-pay.md#configuring-apple-pay-for-digitalriver.js) | [Payment methods in Dashboard](../../administration/dashboard/settings/payment-methods/) |

## How it works

Apple Pay uses a standard payment flow.

## Supported markets <a href="#supported-geographies" id="supported-geographies"></a>

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method/apple-pay/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
