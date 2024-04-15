---
description: >-
  Learn more about the standards related to creating customers and collecting
  tax information.
---

# Customers and tax exemptions

The [checklist items](customers-and-tax-exemptions.md#integration-checklist) and [standards](customers-and-tax-exemptions.md#integration-standards) in this section cover how to collect information from [registered](../../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and [guest](../../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#guest-checkouts-or-invoices) customers. They also take you through the process of handling [tax identifiers](../../../customer-management/setting-tax-related-attributes.md#tax-identifiers) and [tax certificates](../../../customer-management/setting-tax-related-attributes.md#tax-certificates).

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [Does your platform allow customers to create a registered account?](customers-and-tax-exemptions.md#create-an-authenticated-customer)
* [ ] [Do you use your source system's unique customer identifier (UUID) as the Customer `id` when interfacing with the Customers API?](customers-and-tax-exemptions.md#ensure-customer-identifiers-match)
* [ ] [For US-based customers that request a tax-exempt purchase, do you provide the option to apply a tax certificate to the purchase?](customers-and-tax-exemptions.md#provide-customers-the-option-to-apply-a-tax-certificate)
* [ ] [Do you collect and save the necessary tax certificate information?](customers-and-tax-exemptions.md#collect-and-save-tax-certificate-information)
* [ ] [Do you provide the option for non-US based customers to apply a tax identifier to the purchase?](customers-and-tax-exemptions.md#integrate-a-method-for-capturing-tax-identifiers)
* [ ] [Do you implement the necessary element to collect and validate a customer's tax identifier information?](customers-and-tax-exemptions.md#collect-and-validate-tax-identifier-information)
* [ ] [Once a tax identifier is validated, do you save it to the customer's account?](customers-and-tax-exemptions.md#save-a-validated-tax-identifier-to-a-customers-account)

## Integration standards

These integration standards relate to customers and tax exemptions:

### Create an authenticated customer

Your integration must be able to [create a record](../../../customer-management/creating-a-customer.md) for [registered customers](../../../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) who represent either an [individual or a business](../../../customer-management/creating-a-customer.md#customer-type). You can use this record to assign the customer a [default payment method](../../../customer-management/creating-a-customer.md#default-payment-source), [shipping address](../../../customer-management/creating-a-customer.md#shipping-address), and [locale](../../../customer-management/creating-a-customer.md#locale). You can also attach [tax identifiers](../../../customer-management/setting-tax-related-attributes.md#tax-identifiers) and [tax certificates](../../../customer-management/setting-tax-related-attributes.md#tax-certificates) to the customer. A customer can also [request to be forgotten](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/developer-resources/standards-and-certifications/integration-checklists/broken-reference/README.md).

### Ensure customer identifiers match

When you [create a Customer](../../../customer-management/creating-a-customer.md), you can [specify a unique identifier](../../../customer-management/creating-a-customer.md#unique-identifier) for that record. If you don't provide us an identifier, we generate one for you and return it in the response.

We highly recommend that the customer identifier in your commerce system matches the identifier of its corresponding [Customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) in our system. This ensures that the customer is processed correctly during the checkout process.

### Provide customers the option to apply a tax certificate

[Business customers](../../../customer-management/setting-tax-related-attributes.md#customer-type) in the United States with valid [tax certificates](../../../customer-management/setting-tax-related-attributes.md#tax-certificates) may qualify for a tax exemption on their order. Prior to placing an order, your user interface should provide US-based customers the option to apply a tax certificate to their purchase.

### Collect and save tax certificate information

If customers indicate that they want to apply a tax certificate to a purchase, you should provide a file upload prompt and then collect the document. You should also ensure that customers enter the company name, relevant tax authority, start date and end date that are displayed on thecertificate.

If the customer supplies all the required information, [use the Files API to upload the document](../../../order-management/files-and-file-links-1/files.md) to Digital River's servers. Then [add the tax certificate to the customer's account](../../../customer-management/setting-tax-related-attributes.md#adding-a-tax-certificate), ensuring that you send the required company, authority, start date, end date, and file identifier data in the request.

### Provide customers the option to apply a tax identifier <a href="#integrate-a-method-for-capturing-tax-identifiers" id="integrate-a-method-for-capturing-tax-identifiers"></a>

Some [business customers](../../../customer-management/setting-tax-related-attributes.md#customer-type) have [tax identifiers](../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md) that allow them to purchase zero-rated goods. Prior to placing an order, your user interface should provide customers the option to apply a tax identifier to a purchase.

### Collect and validate tax identifier information

If customers indicate that they want to apply a tax identifier to a purchase, implement the [tax identifier element](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/developer-resources/standards-and-certifications/integration-checklists/broken-reference/README.md) to both collect and validate the information.

### Save a validated tax identifier to a customer's account

Once you [validate a tax identifier](../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#validating-tax-identifiers), your integration should [save the tax identifier to the customer's account](../../../integration-options/checkouts/creating-checkouts/tax-identifiers.md#attaching-tax-identifiers-to-customers).

## API interfaces

| Documentation                                                                                                                                            | Direct API                                                                                                          | PHP SDK                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| [Customers](../../../customer-management/customers.md)                                                                                                   | [Customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers)                           | [Customers](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Customer.md)                        |
| [Tax attributes](../../../integration-options/checkouts/creating-checkouts/tax-calculations.md)                                                          |                                                                                                                     |                                                                                                                        |
| [Files](../../../order-management/files-and-file-links-1/files.md)                                                                                       | [Files](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files)                                   | [Files](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/File.md)                                |
| [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started) |                                                                                                                     |                                                                                                                        |
| [DigitalRiver.js Drop-in](../../../payments/payment-integrations-1/drop-in/)                                                                             |                                                                                                                     |                                                                                                                        |
| [Country specs](../../../integration-options/checkouts/creating-checkouts/country-specs.md)                                                              | [Country specifications](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications) | [CountrySpecification](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/CountrySpecification.md) |
