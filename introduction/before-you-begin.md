---
description: >-
  Learn what you need to know before you begin an integration with the
  Salesforce B2B Commerce App.
---

# Before you begin

Familiarity with Salesforce will help when integrating the Salesforce B2B Commerce App with Salesforce.

Salesforce has several sandboxes. When you integrate the Salesforce B2B Commerce App, you need to complete the instructions provided here for each Salesforce Org (production, sandbox, UAT (user acceptance testing), or FULL), and each Digital River site within a Salesforce Org. You can link your developer sandbox to one Digital River site.

## Integration points <a href="#integration-points" id="integration-points"></a>

### 1. Tax estimations <a href="#1-tax-estimations" id="1-tax-estimations"></a>

1. The app extends the global extension point `ccrz.cc_hk_TaxCalculation`.
2. The extension creates a Digital River checkout object based on the Salesforce B2B Commerce cart with product information, prices, and quantity. This checkout request is serialized as JSON and posted to a Digital River web service.
3. The response contains the cart tax amount.

### 2. Payment processing <a href="#2-payment-processing" id="2-payment-processing"></a>

You can integrate payment in multiple locations and flows.

#### **During checkout** <a href="#during-checkout" id="during-checkout"></a>

In the standard checkout flow, you can apply the payment against the order using [Drop-in](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/drop-in). Ask your Digital River Business Development Manager to configure your payment methods.

#### **My Wallet page** <a href="#my-wallet-page" id="my-wallet-page"></a>

* You can add new payment methods and update existing payment methods.
* Only credit card payment methods support saved payment options.

### 3. Disclosures <a href="#3-disclosures" id="3-disclosures"></a>

Digital River requires that you display certain disclosures and related links on the checkout pages and shopper notifications (transactional emails). You can use a [DigitalRiver object](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/digitalriver.js/reference/digitalriver-object) provided by [DigitalRiver.js](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/digitalriver.js) to create various disclosures, Terms of Sale, warranty information, and California Privacy Rights required by Digital River.

### 4. Selling entities <a href="#4-selling-entities" id="4-selling-entities"></a>

The Salesforce B2B Commerce App relies on the Hosted Commerce platform via the Digital River API. See [Selling entities](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/shared-properties/selling-entities) for more information.
