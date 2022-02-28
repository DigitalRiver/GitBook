---
description: Learn how to enable support for digital products.
---

# Step 7: Enable support for digital products

To enable support for digital products, the checkout flow has been changed by extending the `MultiStepCheckoutController.java` and `addCheckoutStepsToModel()` methods in various checkout steps controllers.&#x20;

Products marked as `Digital` in the `DRProductType` attribute of the product configuration will be treated as a digital product in this extension.

See [Step 8: Run the confirmation email body template](step-10-run-the-confirmation-email-body-template.md) for digital product-related changes in the confirmation email.

See [Step 10: Customize the locale, OMS, and webhooks](step-10-customize-the-locale-oms-and-webhooks.md) section for OMS-related changes for digital products.

****
