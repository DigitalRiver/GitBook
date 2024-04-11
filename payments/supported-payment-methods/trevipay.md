---
description: >-
  TreviPay is a B2B net terms line of credit that integrates with e-commerce
  technology to allow invoicing at checkout.
---

# TreviPay

Digital River offers the TreviPay payment method from Multi Service Technology Solutions, Inc.

TreviPay allows you to extend a line of credit for business buyers at checkout. This fully branded solution facilitates online B2B payments by offering flexible net terms, digital statement handling, collections, credit approval management, and improving the overall B2B online buying experience. Digital River supports the following features: create user, payment capabilities, dispute and chargeback, subscription, reporting, API support, fraud, Drop-in payments, term code service support, and tax.

TreviPay assesses creditworthiness, absorbs non-payment risk, including the localized dunning process (collections) if required, and provides online Merchant and Buyer statement management tools. TreviPay supports the following features: application processing, account administration, account self-service, thresholds, commerce experience, alerts, and dunning (collections) if required.

TreviPay processes online e-commerce orders for physical, digital, and recurring product types. TreviPay does not support phone-in orders.

Contact your Customer Success Manager and sign a TreviPay addendum if you want to use TreviPay.

## Benefits

Offering net terms online for business buyers streamlines the legacy accounts receivable and payable processes, alleviates buyer cash flow constraints, and leads to increased buyer loyalty and higher average order values. With this payment method, Merchants remove their credit risk, offload collection responsibilities, and get paid upfront while their buyers pay over time.

## How to configure&#x20;

How you configure TreviPay depends on whether you're using [DigitalRiver.js with Elements](../payment-integrations-1/digitalriver.js/) or [Drop-in payments](../payment-integrations-1/drop-in/).  &#x20;

| DigitalRiver.js with Elements                                                                 | Drop-in payments                                                                          |
| --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [Configuring TreviPay](../payment-integrations-1/digitalriver.js/payment-methods/trevipay.md) | [Payment methods in Dashboard](../../administration/dashboard/settings/payment-methods/)  |

## How it works

Buyers select the TreviPay option at checkout, and then they either log in to the Merchant's profile to complete their purchase or apply for their line of credit. Upon approval, the buyer can complete their transaction and manage purchases, statements, and vendor forms through the buyer portal.

TreviPay uses a [submit then redirect (STR) payment flow](../../integration-options/checkouts/building-you-workflows/handling-redirect-payment-methods.md). Buyers select the TreviPay option at checkout, and then they either log in to the Merchant's profile to complete their purchase or apply for their line of credit. Upon approval, the buyer can complete their transaction and manage purchases, statements, and vendor forms through the buyer portal.

### Promote the TreviPay credit solution

You can set up your storefront to promote the TreviPay credit solution.

<div align="left">

<img src="../../.gitbook/assets/MSTS-store-page.png" alt="">

</div>

### TreviPay enrollment form

You can add a link to the enrollment form on your home page, product page, and checkout page. You can also add a link to the enrollment form from your customer relationship manager (CRM).

When a customer clicks the **Apply Now** button, the information they provide on the Enrollment Application page creates the Admin user.

<div align="left">

<img src="../../.gitbook/assets/Enrollment 1.png" alt="">

</div>

The information provided on the Billing Contact page creates the Payer user.

<div align="left">

<img src="../../.gitbook/assets/Enrollment 2.png" alt="">

</div>

When the customer completes the fields and clicks **Next**, the Credit Application appears.

<div align="left">

<img src="../../.gitbook/assets/MSTS-credit-applications.png" alt="">

</div>

When the client completes and submits the Credit Application, they will see a Congratulations message stating they successfully submitted their application.

<div align="left">

<img src="../../.gitbook/assets/MSTS-congratulations.png" alt="">

</div>

### Phone call

TreviPay will call the customer up to three times to gather information, such as the customer's phone number, so that TreviPay can set up two-factor authentication (2FA) for the customer's account.

### Email notification

The customer will later receive two emails. The first email will say the application has been submitted. The second email will state whether the application for their account has been approved or declined. The validated customer can complete the purchase using two-factor authentication (2FA).

{% hint style="info" %}
TreviPay does not require the customer to sign in to the client portal, but they recommend it.
{% endhint %}

<div align="left">

<img src="../../.gitbook/assets/MSTS-approval-email.png" alt="">

</div>

### TreviPay enrollment URL

Digital River will provide the TreviPay enrollment form URL and redirect URL. You can include the enrollment form link on your homepage, product page, checkout page, or via your customer relationship management (CRM). The format for the enrollment form URL is:\
`https://<progamName>.b2b.credit/<locale>/apply?client_reference_id=<business-UUID>`

**Example:** `https://acmeUS.b2b.credit/en-US/apply?client_reference_id=Acme-123456`

| Attribute             | Description                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<programName>`       | The name of the program. TreviPay URLs are static and mapped to the specific program.                                                                                                                                                                                                                                                                                                                                |
| `client_reference_id` | <p>The business identifier. This is a string without the restriction of character types and can be up to 50 characters in length. Each ecosystem (Digital River API) will be responsible for sending TreviPay a unique <code>client_reference_ID</code> for a shopper enrollment.</p><p>The value for the string is the business's universally unique identifier (UUID) (for example: <code>Acme-123456</code>).</p> |
| `<locale>`            | A designator that combines the two-letter [ISO 639-1](https://en.wikipedia.org/wiki/ISO\_639-1) language code with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code (for example, `en-US`).                                                                                                                                                                                 |

### Including the e-commerce URL in the enrollment URL

Include an `ecommerce_url` in the enrollment form URL when redirecting the customer to the TreviPay enrollment form. The format for the enrollment form with a redirect is as follows:

`https://<white-label>.b2b.credit/<locale>/apply?client_reference_id=<business-UUID>&ecommerce_url=<www.returnURL.com>`

#### **Example**:

`https://acmeUS.b2b.credit/<locale>/apply?client_reference_id=Acme-123456&ecommerce_url=www.acme-returnURL.com`

| Attribute       | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| `ecommerce_url` | The redirect URL to your website (for example, www.acme-returnURL.com). |

You must include a `client_reference_id` with the return URL when redirecting to the TreviPay enrollment form.

## Support matrix

<table><thead><tr><th width="233.33333333333331">Basics</th><th>Customer</th><th>Redirect</th></tr></thead><tbody><tr><td></td><td>Payment Type</td><td>Buy Now Pay Later B2B</td></tr><tr><td>Requirements</td><td>Addendum</td><td>Yes</td></tr><tr><td>Supported Product Types</td><td>Physical / Digital</td><td>Both</td></tr><tr><td></td><td>Captures Funds when Physical Product Shipped or Digital Product Downloaded</td><td>Yes</td></tr><tr><td></td><td>Chargeback</td><td>Yes</td></tr><tr><td></td><td>Standard / Premium</td><td>Premium</td></tr><tr><td></td><td>Multiple / Partial</td><td>Yes</td></tr><tr><td></td><td>Recurring Payments</td><td>Yes</td></tr></tbody></table>

## Supported markets <a href="#supported-geographies" id="supported-geographies"></a>

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method/trevipay/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
