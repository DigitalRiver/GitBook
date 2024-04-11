---
description: >-
  Gain a better understanding of the Merchant of Record/Seller of Record
  compliance requirements.
---

# Compliance requirements

Every ecommerce store and application built using the [Digital River API](../../) must meet certain [Merchant of Record/Seller of Record (MOR/SOR)](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements. This ensures that all legal and regulatory obligations are satisfied before deployment, thus allowing Digital River to safely assume the MOR/SOR risks.

Among other topics, these compliance requirements cover:

* Displays and disclosures
* Payment methods
* Subscriptions and auto-renewals
* Order verification and review
* Taxes and regulatory fees
* Import/export controls
* Prohibited goods and services
* Prohibited countries
* Fraud screening
* Supported fulfillment models

When legal and permissible, you're allowed to deviate from these requirements. However, if your implementation doesn't adhere to them, and Digital River must defend itself before a regulatory body dealing with, for example, information privacy or tax issues, then you're responsible to protect Digital River from the consequences of your deviation from either the requirements or our terms of service.

When building your tool, we recommend you use our [integration checklists](integration-checklists/). By adhering to the standards outlined within each, you'll be better positioned to pass both your [tool certification](certification-process.md) and [store compliance review](compliance-requirements.md#store-compliance-review).

## Store compliance review

Once you've used [our checklists](integration-checklists/) to build your integrated tool and you've completed the [certification process](certification-process.md), the tool is almost ready for deployment to client sites. However, before any client store that uses your tool can go into production, you must:

* Create a [client-specific Digital River API account](../../administration/dashboard/account/adding-an-account.md). By doing so, you separate this client's objects from the objects of your other clients.
* Configure the client-specific API account with the integration tool you built for the store.
* Conduct any optional configurations, such as the [Drop-in payments](../../payments/payment-integrations-1/drop-in/) plugin, based on the Digital River features you're employing
* Carry out a [production checkout certification](compliance-requirements.md#production-checkout-certification) to ensure the client site meets all [MOR/SOR](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements

### Production checkout certification

Prior to a client site's deployment, Digital River performs an official production checkout certification. During this process, Digital River works with you and your client to ensure the client store meets all [MOR/SOR](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements and that both you and Digital River are protected. We also determine whether any compliance requirement exceptions are warranted.

## Learning tools

For those looking to better understand our [MOR/SOR](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements, we provide an [interactive compliance tool](compliance-requirements.md#interactive-compliance-tool), as well as numerous articles detailing our [guidelines and best practices](compliance-requirements.md#guidelines-and-best-practices). In all of these learning resources, you'll find the compliance details labeled as either _required_, _recommended_, or _informational_.

### Interactive compliance tool

To help developers and product managers better understand the [MOR/SOR](../glossary.md#merchant-of-record-seller-of-record-mor-sor) requirements, Digital River provides an [interactive compliance tool](https://drapi.io/ecommguidance/) (_refer to_ [_Accessing the learning tools_](compliance-requirements.md#accessing-the-learning-tools) _for access information)_.

The compliance tool allows you to navigate through various pages typically included in a [checkout experience](../../integration-options/checkouts/#checkout-experience). On each page, you can click tooltips to learn more about the related display or implementation requirements. To gain an even deeper understanding of the full requirements, you can browse the articles linked to from each tooltip.

### Guidelines and best practices

The [guidelines and best practices](https://digitalriver.service-now.com/kb?id=kb\_search\&kb\_knowledge\_base=6af4828d1b005410fd31964ead4bcb52) (_refer to_ [_Accessing the learning tools_](compliance-requirements.md#accessing-the-learning-tools) _for access information)_ within the Knowledge Portal provide resources designed to help Digital River employees, clients, prospects, and partners understand important information they need to know. The Knowledge Portal itself contains various Knowledge Bases that each have unique purposes and audiences. Within each Knowledge Base, there are articles on a wide range of topics which can all be found by performing a keyword search.

### Accessing the learning tools

Access to the [learning tools](compliance-requirements.md#learning-tools) is only granted to clients, partners, and prospective clients who have signed a non-disclosure agreement with Digital River. Existing clients, partners and prospective clients should contact their account managers to get the access instructions.

Prospective clients can start the process by [requesting a demo](https://www.digitalriver.com/request-demo/).

To discuss partnership opportunities with Digital River, please [contact us](https://www.digitalriver.com/partner-with-us/).
