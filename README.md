---
description: >-
  Use the Digital River Salesforce B2C LINK Cartridge to manage global payments
  and act as your risk management solution.
---

# Salesforce B2C LINK Cartridge 2.2

## System requirements

* **Digital River LINK Cartridge version:** 22.1.0&#x20;
* **API Fleet and version**: Digital River version 2021-03-23.
* **Commerce Platform Version**: This package was implemented against SF B2C version 21.1 and tested against compatibility mode 21.7. This package was developed against SFRA versions  6.0.0.
* The cartridge only supports SFRA. This cartridge is not supported with SiteGenesis.

## Upgrade path&#x20;

To upgrade from 1.0, 2.0, 2.1, or 2.1.1, complete all steps under <mark style="color:green;"></mark> [Install the Salesforce B2C LINK Cartridge](install-the-salesforce-b2c-link-cartridge.md).

## Before you begin

Before you can install the Salesforce B2C LINK Cartridge, you'll need to contact Digital River, [salesforce@digitalriver.com](mailto:salesforce@digitalriver.com) to request credentials, configure the available payment options within Drop-in, and receive your LINK key. Additionally:

* Use of the Digital River cartridge requires credentials and keys from Digital River (contact Digital River at [salesforce@digitalriver.com](mailto:salesforce@digitalriver.com)).
* The cartridge is designed for the US locale and is compatible with any locale if you add the localization strings.

## Limitations

The following Salesforce Commerce Cloud (SFCC) features are not supported:

* SFCC supports a single Ship To address and a single Ship From address per site. SFCC does not support multiple Ship To and Ship From addresses. You can configure the Ship From address in the Business Manager under [site preferences](configure-the-salesforce-b2c-link-cartridge.md#custom-site-preferences). The system provides the Ship To addresses during the checkout process.
* When a customer stores a credit card in the account, the system stores card data on the Digital River service. If you disable Digital River, the shopper cannot use the stored cards to pay for orders. The shopper will have to add them to their account again.

## Firewall requirements

No adjustments to the SFCC Firewall settings are needed.
