---
description: >-
  Learn about the components for the Digital River Salesforce B2C LINK
  Cartridge.
---

# Component overview

## Functional overview

The Salesforce B2C LINK Cartridge package contains three cartridges:

* [bm\_digitalriver](component-overview.md#bm\_digitalriver)
* [int\_digitalriver](component-overview.md#int\_digitalriver)
* [int\_digitalriver\_sfra](component-overview.md#int\_digitalriver\_sfra)

### bm\_digitalriver&#x20;

A Business Manager extension cartridge (bm\_digitalriver) will communicate with DigitalRiver services and report if they are up or down. These include static requests that use the REST API to send a payload to the Digital River services. The response is then checked to see if the service returns an expected successful response.

### int\_digitalriver&#x20;

Integration cartridge containing API integrations that form requests, parse responses, and update objects.

### int\_digitalriver\_sfra

A second integration cartridge (int\_digitalriver\_sfra) delivers adjustments and extensions to existing storefront functionality. By separating the storefront functionality from the back-end, minimal code changes will be necessary.

## Supported payment methods

The Salesforce B2C LINK Cartridge for Commerce Cloud supports the following payment methods:

* Credit Cards
* PayPal
* ApplePay

## Limitations, constraints

You can add additional payment methods not included out of the box as needed.

The following Salesforce Commerce Cloud (SFCC) features are not supported:

* Multiple Shipping Addresses

## Compatibility

This package was implemented against SF B2C Version 20.1.

## Privacy, payment

This cartridge accesses customer profile data to send the SFCC Customer ID and email to Digital River.

Digital River provides PCI compliance, tokenization, and fraud screening through an API reference. When the shopper enters payment information at checkout, they interact with secure payment fields that are hosted by Digital River within a Salesforce-hosted page. The shopper is never redirected to another page. Those secure fields are served up by [DigitalRiver.js](https://docs.digitalriver.com/commerce-api/payment-integrations-1/digitalriver.js), a developer-friendly library that allows brands to securely process transactions without having to take on the responsibilities of PCI compliance. When brands use the DigitalRiver.js API reference on their Salesforce store, Digital River serves up payment methods, validates card data, tokenizes customer information, performs fraud screening, collects sensitive card data, and processes transactions in a manner that is fully compliant with the Payment Card Industry Data Security Standards (PCI DSS). Digital River is a Level 1 PCI compliant service provider. Customer data is stored on Digital River’s secure servers, never on Salesforce servers. The service does not allow PCI data to hit the Salesforce server.
