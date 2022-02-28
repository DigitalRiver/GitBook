---
description: >-
  Use the Digital River Salesforce B2C LINK Cartridge to manage global payments
  and act as your risk management solution.
---

# Salesforce B2C LINK Cartridge 2.1

## System requirements

* **LINK Cartridge version:** 21.2.0
* **API Fleet and version**: Digital River version 2021-02-23.
* **Commerce Platform Version**: This package was implemented against SF B2C version 21.5 and tested against compatibility mode 19.10. This package was developed against SFRA versions 5.3.0 and 6.0.0.
* The cartridge only supports SFRA. This cartridge is not supported with SiteGenesis.

## Upgrade Path&#x20;

To upgrade from 1.0 or 2.0, complete all steps under [Install the Salesforce B2C LINK Cartridge](install-the-salesforce-b2c-link-cartridge.md).

## Before you begin

Before you can install the Salesforce B2C LINK Cartridge, you'll need to contact Digital River, [salesforce@digitalriver.com](mailto:salesforce@digitalriver.com) to request credentials, configure the available payment options within Drop-in, and receive your LINK key. Additionally:

* Use of the Digital River cartridge requires credentials and keys from Digital River (contact Digital River at [salesforce@digitalriver.com](mailto:salesforce@digitalriver.com)).
* The cartridge is designed for the US locale and is compatible with any locale if you add the localization strings.

## Limitations

The following Salesforce Commerce Cloud (SFCC) features are not supported:

* Tested for a single Ship To address and single Ship From address per site. SFCC does not support multiple Ship To and Ship From addresses. You can configure the Ship From address in the Business Manager under site preferences. The Ship To addresses is provided during the checkout process.
* When a customer stores a credit card in the Account, the card data is stored on the Digital River service, hence if you turn off Digital River the customer will not be able to pay with stored cards and will have to add them to the Account again.

## Firewall requirements

No adjustments to the SFCC Firewall settings are needed.
