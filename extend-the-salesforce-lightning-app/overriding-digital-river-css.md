---
description: Learn how to override the Digital River CSS.
---

# Overriding Digital River CSS

The Digital River app provides an extension point to override the style for components that load through the VF page in which Digital River CSS  is loaded.

Load the following components through the VisualForce (VF) page: &#x20;

* `drb2b_drTermsElement`
* `drb2b_taxIdentifier`
* `drb2b_payments`
* `drb2b_dropIn`
* `drb2b_newPayments`
* `drb2b_myWalletPayment`
* `drb2b_myWallet`
* `drb2b_myTaxIdentifier`

The Digital River App provides a configuration called [Client Custom CSS Static Resource](../integrate-the-salesforce-lightning-app/step-2-configure-the-digital-river-app.md#configure-the-general-config-settings). To override the Digital River CSS (which is part of the managed package), create a new custom static resource with a custom CSS file and configure its name in the Digital River App settings.

You should use the CSS classes that are part of the Digital River CSS in the custom CSS file to override the Digital River CSS which is part of the managed package.

{% code title="Sample code" %}
```html
.DR-button-text{text-transform:uppercase;background-color:purple !important}
```
{% endcode %}

In general, you can overwrite classes that start with `DR`.  You should overwrite other classes including salesforce classes (that is, classes that start with `slds`) in Experience Builder.

{% hint style="info" %}
Make sure your CSS has a higher specificity value to ensure your CSS  overrides the existing CSS.
{% endhint %}
