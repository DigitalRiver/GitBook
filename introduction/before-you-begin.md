---
description: >-
  Learn what you need to know before you begin an integration with the
  Salesforce B2B Commerce App.
---

# Before you begin

Familiarity with Salesforce will help when integrating the Salesforce B2B Commerce App with Salesforce.

Salesforce has several sandboxes. When you integrate Digital River with the Salesforce B2B Commerce App, you need to complete the instructions provided here for each Salesforce Org (production, sandbox, UAT (user acceptance testing), or FULL), and each Digital River site within a Salesforce Org. You can link your developer sandbox to one Digital River site.

## Integration points

### 1. Tax estimations

1. The app extends the global extension point `ccrz.cc_hk_TaxCalculation`.
2. The extension creates a Digital River cart based on the Salesforce B2B Commerce cart with product information, prices, and quantity. This cart is serialized as a JSON object, encrypted, and posted to a Digital River web service.
3. The response contains the cart tax amount.

### 2. Payment processing

You can integrate payment in multiple locations and flows.

#### **During checkout**

In the standard checkout flow, you can apply the payment against the order using one of the following methods:

* Credit Card
* PayPal
* Purchase Order
* Previously stored payment method

#### **My Wallet page**

* You can add new payment methods and update existing payment methods.
* Only credit card payment methods support saved payment options.

### 3. Disclosures

Digital River requires that you display certain disclosures and related links on the checkout pages and shopper notifications (transactional emails). You can use [DigitalRiver object](https://docs.digitalriver.com/commerce-api/payment-integrations-1/digitalriver.js/reference/digitalriver-object) provided by [DigitalRiver.js](https://docs.digitalriver.com/commerce-api/payment-integrations-1/digitalriver.js) to create various disclosures, Terms of Sale, warranty information, and California Privacy Rights required by Digital River.

### 4. Selling entities <a href="#4-selling-entities" id="4-selling-entities"></a>

The Salesforce B2B Commerce App relies on the Hosted Commerce platform via the Commerce API. See [Selling entities](https://docs.digitalriver.com/commerce-api/orders-1/selling-entities) for more information.
