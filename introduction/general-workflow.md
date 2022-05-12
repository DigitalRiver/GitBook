---
description: Learn more about installing the connector cartridges and secure payments.
---

# General workflow

## Install the connector cartridges <a href="#install-the-connector-cartridges" id="install-the-connector-cartridges"></a>

The Salesforce B2C LINK Cartridge package contains three cartridges with the [Drop-in](https://docs.digitalriver.com/digital-river-api/payments/payment-integrations-1/drop-in) functionality for Storefront Reference Architecture (SFRA):

* [bm\_digitalriver](https://app.gitbook.com/@digital-river/s/salesforce-b2c-draft/\~/drafts/-MPjXhMIoSRjoBcAnaPW/v/2.0.0/general-workflow#bm\_digitalriver)
* [int\_digitalriver](https://app.gitbook.com/@digital-river/s/salesforce-b2c-draft/\~/drafts/-MPjXhMIoSRjoBcAnaPW/v/2.0.0/general-workflow#int\_digitalriver)
* [int\_digitalriver\_sfra](https://app.gitbook.com/@digital-river/s/salesforce-b2c-draft/\~/drafts/-MPjXhMIoSRjoBcAnaPW/v/2.0.0/general-workflow#int\_digitalriver\_sfra)
* [int\_digitalriver\_webhooks](general-workflow.md#int\_digitalriver\_webhooks)

### bm\_digitalriver <a href="#bm_digitalriver" id="bm_digitalriver"></a>

The Business Manager extension cartridge:

* Communicates with Digital River services and reports if they are up or down. These include static requests that use the REST API to send a payload to the Digital River services. Check the response to see if the service returns an expected successful response.
* Gives permission to execute jobs. The text label on the job status button indicates the job can be launched or that it is being executed. See section [Business Manager Roles & Permissions](../configure-the-salesforce-b2c-link-cartridge.md#business-manager-roles-and-permissions) about adding the context menu item to a role.

### int\_digitalriver <a href="#int_digitalriver" id="int_digitalriver"></a>

This integration cartridge contains API integrations that form requests, parse responses, and updates objects.

### int\_digitalriver\_sfra <a href="#int_digitalriver_sfra" id="int_digitalriver_sfra"></a>

This integration cartridge delivers adjustments and extensions to existing storefront functionality.&#x20;

![](<../.gitbook/assets/CARTRI\_1 (1).png>)

### int\_digitalriver\_webhooks

This integration cartridge process Digital River webhook requests and optionally sends email notifications.

## Checkout flow

The following sequence diagram shows the checkout interaction between the Shopper, Salesforce B2C Commerce, the Salesforce B2C Commerce App, and Digital River.

{% file src="../.gitbook/assets/salesforceB2C_sequencediagram-v2.1.png" %}
SalesforceB2C\_sequencediagram-V2.1.png
{% endfile %}

## US tax exemption flow <a href="#privacy-and-payments" id="privacy-and-payments"></a>

The following sequence diagram shows the US tax exemption interaction between the Shopper, Salesforce B2C Commerce, the Salesforce B2C Commerce App, and Digital River.

{% file src="../.gitbook/assets/SalesforceB2C_USTaxExemptionFlow-2.1 (1).png" %}
SalesforceB2CUSTaxExemptionFlow-2.1.png
{% endfile %}

## Tax identifier flow

The following sequence diagram shows the tax identifier interaction between the Shopper, Salesforce B2C Commerce, the Salesforce B2C Commerce App, and Digital River.

{% file src="../.gitbook/assets/salesforceB2C_TaxIdentifierFlow-2.1.png" %}
SalesforceB2C\_TaxIdentifierFlow-2.1.png
{% endfile %}

## Privacy and payments <a href="#privacy-and-payments" id="privacy-and-payments"></a>

This cartridge accesses customer profile data to send the SFCC Customer ID and email to Digital River.

Digital River provides Payment Card Industry (PCI) compliance, tokenization, and fraud screening through an API reference (Digital River is a Level 1 PCI-compliant service provider).

Enter payment information at checkout to interact with secure payment fields—DigitalRiver.js provides the secure fields within a Salesforce-hosted page; Digital River never redirects a shopper to another page.

When brands use this cartridge on their Salesforce store, Digital River:

* Provides payment methods
* Validates card data
* Tokenizes customer information
* Performs fraud screening
* Collects sensitive card data
* Processes transactions in a manner that is fully compliant with the Payment Card Industry Data Security Standards (PCI DSS).

Customer payment data is stored on Digital River’s secure servers, never on Salesforce servers.

For additional privacy information, contact your Digital River Account Manager.
