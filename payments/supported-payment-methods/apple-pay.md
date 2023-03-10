---
description: >-
  Apple Pay provides a fast and secure shopping experience where the consumer
  can quickly and seamlessly checkout with their Apple Touch authentication
  without login details or credentials.
---

# Apple Pay

A fast and secure shopping experience where the consumer can quickly and seamlessly checkout with their Apple Touch authentication without login details or credentials. Digital River will support Apple Pay as a payment method on the payment service and DigitalRiver.js. Apple Pay is currently available to consumers in 21 countries and currently is supported only on IOS devices (iPhones, Macs, and so on).&#x20;

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/applepay.html) (only viewable on Apple devices).

## How to configure

To offer Apple Pay on your website, you first need to validate your domain with Apple before you can accept transactions. To complete this validation:

1. [Download](https://drapi.io/docs/apple-pay/apple-developer-merchantid-domain-association) the `apple-developer-merchantid-domain-association` file.
2. Save the file to the following location on the domain where you want to offer Apple Pay: `/.well-known/apple-developer-merchantid-domain-association` \
   \
   Repeat this step for each additional domain where you want to offer Apple Pay. For example:\
   `https://buy.mydomain.com/.well-known/apple-developer-merchantid-domain-association`\
   `https://shop.mydomain.com/.well-known/apple-developer-merchantid-domain-association`\
   `https://www.mydomain.com/.well-known/apple-developer-merchantid-domain-association` \
   \
   **Note**: You must serve the `apple-developer-merchantid-domain-association` file over HTTPS.
3. Contact your Digital River representative with the list of domains you want to register.

After completing these steps, the remainder of the Apple Pay configuration process depends on whether you're using [DigitalRiver.js with Elements](../payments-solutions/digitalriver.js/) or[ Drop-in payments](../payments-solutions/drop-in/).

| DigitalRiver.js with Elements                                                               | Drop-in payments                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| [Configuring Apple Pay](../payments-solutions/digitalriver.js/payment-methods/apple-pay.md) | [Drop-in Payments Integration Guide](../payments-solutions/drop-in/drop-in-integration-guide.md) |

## Supported markets <a href="#supported-geographies" id="supported-geographies"></a>

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
