---
description: Learn about Digital River's build standards and certification process.
---

# Standards and certifications

You can work with Digital River to create a connector that meets our build standards, conduct [tool-specific](certification-process.md) and [store-specific](compliance-requirements.md#store-compliance-review) certifications, and then deploy the connector to end sites. The following pages explain how to navigate this process:

* [Certification process](certification-process.md): A high-level and [detailed](certification-process.md#detailed-certification-process) explanation of how to certify your commerce connector tool.
* [Compliance requirements](compliance-requirements.md): An introduction to the [Merchant of Record/Seller of Record (MOR/SOR)](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements that your tool and the client sites it implements must meet. This section also describes the [store compliance review](compliance-requirements.md#store-compliance-review) and previews the [learning tools](compliance-requirements.md#learning-tools) we provide you to better understand the MOR/SOR requirements.
* [Integration checklists](integration-checklists/): A set of checklists that cover important Digital River features your commerce connector should integrate.
* [Test and use cases](test-and-use-cases.md): Unique cases that you can use to build and test your connector.

By adhering to these standards and completing these certifications, you can take advantage of our commerce and payment products. More specifically, you'll be able to create certified, reusable components that integrate Digital River features into your platform and then deploy them across your client base.

## Target audience

The standards and certifications outlined here are intended for [product managers](./#product-managers), [platform developers](./#platform-developers-and-engineers), and [QA teams](./#qa-teams) who want to learn how to integrate with Digital River.

### Product managers

Product managers can use these build standards to:

* Obtain the big picture on the [order lifecycle, payments processing, and fulfillment chains](../../integration-options/checkouts/process-flow.md)
* Understand how the [commerce connector certification process](certification-process.md) works
* Develop strategies for [implementing client end sites](certification-process.md#end-site-implementations) that are [MOR/SOR](../glossary.md#merchant-of-record-seller-of-record-mor-sor) compliant
* Learn how to direct the different teams collaborating on these implementations
* Organize and determine how to accomplish the following build tasks:
  * [Initial interactions and partner contracts](./#initial-interactions)
  * [Tool planning](certification-process.md#planning-and-prerequisites) and [development](certification-process.md#tool-development)
  * [Tool submission and certification](certification-process.md#tool-submission-and-certification)
  * [Implementing end sites with the certified tool](certification-process.md#end-site-implementations)

### Platform developers and engineers

Platform developers and engineers can use these build standards to:

* Understand fundamental coding principles and the available Digital River APIs
* Learn [how to create API accounts](../../administration/dashboard/quick-start-guide.md#step-1-creating-a-test-account) using the Digital River [Dashboard](../../administration/dashboard/)
* Determine how to [configure webhooks](../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) that allow you to respond to [Digital River events](../../order-management/events-and-webhooks-1/events-1/event-types.md)
* Acquire a better understanding of:
  * [Products](../../product-management/skus.md)
  * [Customers](../../customer-management/customers.md)
  * [Checkouts](../../integration-options/checkouts/creating-checkouts/)
  * [Orders](../../order-management/creating-and-updating-an-order.md)
  * [Drop-in payment acceptance](../../payments/payment-integrations-1/drop-in/)
  * [Fulfillments and cancellations](../../order-management/fulfillments.md)
  * [Post-fulfillment returns and refunds](../../order-management/returns-and-refunds-1/)
* Understand the purpose of the [MOR/SOR compliance](compliance-requirements.md) process
* Conduct technical code reviews during tool [planning](certification-process.md#planning-and-prerequisites), [development](certification-process.md#tool-development), and [certification](certification-process.md#tool-submission-and-certification)
* [Implement end sites](certification-process.md#end-site-implementations) during the MOR/SOR compliance process

### QA teams

Members of QA teams can use these build standards to:

* Determine appropriate tests for a [variety of use cases](test-and-use-cases.md) that are based on your platform's preferred testing method
* Work with development teams to ensure you're ready for the [certification process](certification-process.md)
* Ensure all [client end sites pass certification](compliance-requirements.md#store-compliance-review)
* Understand [common integration scenarios](integration-checklists/) that cover pre-certification (i.e., not specific to a client) and post-certification, as each client's end site is built and deployed.

## Initial interactions

You can learn more about our current technology partners and system integrators [here](https://www.digitalriver.com/partners/).

If you're already a Digital River partner, we encourage you to access [our partner portal](https://digitalriver.allbound.com). And if you'd like to become a Digital River partner, please [contact us](https://www.digitalriver.com/partner-with-us/).

## Resources

Here you'll find important resources to assist you in building your commerce connector, such as helper libraries, compliance guides, a Postman collection, and [fundamental information](./#digital-river-api-fundamentals) on the Digital River API. You'll also find a list of [common terms](./#common-terms) and their frequently used aliases.

* [Digital River API documentation](../../)
* [Digital River API reference](https://www.digitalriver.com/docs/digital-river-api-reference/)
* [PHP SDK documentation](https://github.com/DigitalRiver/digital-river-php)
* [Digital River Postman collection](https://github.com/DigitalRiver/api-sandbox)
* [Digital River Dashboard](https://dashboard.digitalriver.com)
* [Interactive MOR/SOR compliance guide](https://drapi.io/ecommguidance/) ([_access required_](compliance-requirements.md#accessing-the-learning-tools))

### Digital River API fundamentals

* [Basic information](../../)
* [Dashboard overview](../../administration/dashboard/)
* [Dashboard quick start guide](../../administration/dashboard/quick-start-guide.md)
* [Events](../../order-management/events-and-webhooks-1/events-1/) and [webhooks](../../order-management/events-and-webhooks-1/webhooks/)
* [Error handling](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-types)
* [Basic sequence and interactions](../../integration-options/checkouts/process-flow.md)
* [Products and product identifier mapping](../../product-management/skus.md)
* [Customers](../../customer-management/customers.md) and [tax exemptions](../../customer-management/setting-tax-related-attributes.md)
* [Pre-checkout](../../integration-options/checkouts/process-flow.md#pre-checkout) and [checkout experience](../../integration-options/checkouts/process-flow.md#creating-a-checkout)
* [Payments processing](../../integration-options/checkouts/process-flow.md#creating-a-source-and-order)
* [Strong customer authentication](../../payments/psd2-and-sca/)
* [Recurring billing and subscriptions](../../integration-options/checkouts/subscriptions/subscription-information-1.md)
* [Invoices](../../integration-options/checkouts/subscriptions/invoices.md) and [files](broken-reference)
* [Fulfillments and cancellations](../../order-management/fulfillments.md)
* [Returns and refunds](integration-checklists/reversals.md)

### Common terms

| Term                  | Aliases                                 |
| --------------------- | --------------------------------------- |
| Integration           | Tool, Certified integration, Connector  |
| Commerce provider     | Systems integrator, Platform, Ecosystem |
| Client implementation | End site, Checkout experience, Store    |
