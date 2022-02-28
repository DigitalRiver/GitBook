---
description: >-
  Learn how to operate and maintain the Digital River Salesforce B2C LINK
  Cartridge.
---

# Operations and maintenance

## Data storage

Outside of Commerce Cloud, Digital River API stores Customer, Order, and SKU data across three areas:

|                                          | SOC Compliant                              | PCI Compliant                              |
| ---------------------------------------- | ------------------------------------------ | ------------------------------------------ |
| CPG Payments                             | ​![](.gitbook/assets/image.png)            | ![](.gitbook/assets/Checkmark.png)         |
| Commerce engine for Global Commerce (GC) | ​![](<.gitbook/assets/Checkmark (1).png>)  | ​![](<.gitbook/assets/Checkmark (2).png>)  |
| Payments Service (PC)                    | ​                                          | ​![](<.gitbook/assets/Checkmark (3).png>)  |

The location is Elastic Search, Oracle, and Cassandra, and the duration is a maximum of 10 years for Customer Data and Order Data except for the EU “Right to be forgotten” GDPR requirements, which we support.

## Availability

Services should always be available.

If services are not available, orders and payments cannot be processed.

A provided Business Manager extension cartridge will give real-time status on available services by sending a static request and evaluating the response code sent back to SFCC.

DigitalRiver.js and Digital River API are available globally. Digital River API is available via all three of Digital River’s data centers – Virginia, Oregon, and Ireland. Our load balancers handle fallback.

Digital River’s general availability goal is to respond in 800 ms or less within the Digital River network. The roundtrip response time, which includes external networks, may vary (as expected).

Monitoring with Zabbix is in place, and the Digital River Operations team has logging and notifications in place; Digital River customer-facing teams have access to that data.

## Failover/Recovery process

If there is a service disruption, it will impact the ecommerce experience in the following ways:

1. Payment Methods will not render in the cart during checkout.
2. Tax calculations will not return to the cart.
3. Overall customers will be unable to transact on the ecommerce store, which is leveraging Digital River for tax, payments, and risk.
