---
description: Find answers to common questions.
---

# Common questions

## Pricing and Fees

### What fees are associated with the gateway?

[Contact the Digital River Sales team](https://www.digitalriver.com/request-demo/) for information.

## Account Eligibility

### What currencies and countries does the payment gateway support?

The store must be based in one of the following countries: CA, GL, PM, TC, US, AD, AT, BE, DK, FO, FI, FR, DE, GB, GR, IE, IS, IT, LI, LU, MC, NL, NO, PT, SM, ES, SJ, SE, CH, VA, AL, BY, BG, HR, CZ, EE, HU, KZ, LV, LT, MK, PL, RO, RU, RS, SK, SI, TM, TR, UA, UZ, AF, AZ, DZ, BH, BA, CY, ET, EG, IL, IQ, JO, KE, KW, LB, LS, LY, MR, MT, MA, NG, OM, PK, QA, RE, SA, SL, ZA, TA, TN, AE, YE, AR, BO, BR, CO, CL, CR, DO, EC, GF, GT, HN, MX, NI, PA, PY, PE, PR, SV, TT, UY, VE, AU, AS, BV, IO, NZ, JP, CN, CX, CC, CK, GU, HM, HK, KI, MO, MH, FM, NU, NF, MP, NP, PN, GS, LK, IN, BD, KR, TW, TK, TV, UM, SG, BN, ID, TL, PH, MY, MY, KH, LA, MM, TH, VN

The selected payment method determines the supported currencies.

### What items are restricted for merchants to sell?

For a list of allowed goods, see [Tax codes](https://docs.digitalriver.com/digital-river-api/skus/creating-and-updating-skus#tax-code).

## Transactions&#x20;

### After I create an account, what is the waiting period before I can process transactions?

Assuming the following statements are true, you can start accepting payment on your store through Digital River immediately:

* You are on a BigCommerce paid plan.
* The [Digital River Payments, Fraud, Tax & Compliance Management app is installed](install-the-digital-river-app.md) on your store.
* You [created a Digital River account](https://docs.digitalriver.com/digital-river-api/administration/dashboard/quick-start-guide#step-1-creating-a-free-test-account).
* Digital River has [passed your certification](https://docs.digitalriver.com/digital-river-api/getting-started-1/standards-and-certifications/certification-process). You will work with a Digital River Project Manager to set a timeline launch, including scheduling Checkout Certification.

### How long until the funds are transferred to my bank?

Contact Digital River for more information. Details will be provided in your Digital River contract.

### Will I or my customers receive an additional email or invoice from the payment gateway?

BigCommerce sends the [invoice email](https://support.bigcommerce.com/s/article/Invoices?language=en\_US#default). Digital River does not send the invoice email.

## Orders

### How do I troubleshoot an order?

See [Troubleshooting Orders](https://support.bigcommerce.com/s/article/Troubleshooting-Orders?language=en\_US).

## Refunds

### How soon after a transaction can I perform a refund?

See [Issuing Refunds](https://docs.digitalriver.com/digital-river-api/returns-and-refunds-1/refunds/issuing-refunds).

### Is there an amount of time after which I cannot perform a refund?

&#x20;See [Issuing Refunds](https://docs.digitalriver.com/digital-river-api/returns-and-refunds-1/refunds/issuing-refunds).

### Are there any fees for chargebacks and refunds?

* Fee for **Digital River Payments, Fraud, Tax & Compliance Management app:**  No charge**.**
* Cost for Services Associated with Digital River **** app usage: **** Custom Pricing.  For more information, contact [bigcommerce@digitalriver.com](mailto:bigcommerce@digitalriver.com)
* For questions regarding chargebacks and refunds, contact [bigcommerce@digitalriver.com](mailto:bigcommerce@digitalriver.com).

### What are the limitations around refunds?

Once you [apply an order level refund](https://support.bigcommerce.com/s/article/Processing-Refunds?language=en\_US#refund-order), you may then only refund the remaining order amount afterward. If you **Refund individual items** at this point, you will receive an error.&#x20;

If you want to issue a refund for fees, or importer of record (IOR) tax and duties for cross-border orders, you must initiate this refund from within Digital River.

### Does the integration support [multiple shipments](https://support.bigcommerce.com/s/article/Shipments) to the same location?

Yes.

### Does the integration support [multiple shipments](https://support.bigcommerce.com/s/article/Shipments) to different locations?

No. Digital River only supports multiple shipments when shipping all items on the order to the same location. Digital River only supports one tax calculation per order. As a result, Digital River does not support shipping multiple items from a single order to different locations. That’s because each location applies taxes differently.

### Does the Digital River payment integration automatically check if I have the correct app installed?

Once you download the Digital River **** app from the marketplace, Big Commerce will display all the relevant settings for the storefront. If you do not configure the app settings and ONLY configure the payment settings, there is no additional validation that will flag the store admin that something was not set up for the app to work.

## Additional Features&#x20;

### Are there any fraud filtering options available?

No. Fraud filtering is done automatically by Digital River. See [Fraud prevention and security](3d-secure.md).

### Does it allow authorize-only or recurring/subscription payments?

Authorize-only is supported. Subscriptions are not supported.

## Troubleshooting and payment disputes

### Why did my client receive an error when trying to pay?

&#x20;See Digital River’s [Error handling](https://docs.digitalriver.com/digital-river-api/getting-started-1/standards-and-certifications/integration-checklists/error-handling).

### How are payment disputes handled?

Digital River will handle chargebacks. Other payment disputes (that is, damaged product on delivery) will need to be handled by the merchant. ****&#x20;

During the implementation process with your Digital River project manager, you will be set up with access to the Solutions Center and introduced to your Digital River direct contacts.

### How do I contact the payment gateway’s support?

To find contact information, click [Support](support.md).

### Can I use my VAT ID in order to get a tax exemption?

No. The integration does not support VAT ID.

&#x20;
