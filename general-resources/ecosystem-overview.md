---
description: >-
  Gain a high-level understanding of how client and commerce ecosystems
  integrate.
---

# Commerce infrastructure

The following diagram provides an overview of common architecture used when integrating with Digital River's [Global Seller Services](https://www.digitalriver.com/global-seller-services/). At a high-level, these integrations consist of a client and commerce ecosystem.

![](<../.gitbook/assets/ecosystem-3 (1).png>)

For each step in an integration's workflow, the following provides a more detailed explanation:

1. Core Services integrate with the Commerce Platform (CP) and Online Properties to handle identity management, MyAccount, and data synchronization services.
2. Online Properties supports the customer's MyAccount self-service and browse services.
3. Any customer actions that may result in a transaction are redirected to the CP storefront.
4. For all incoming traffic, the CP's storefront manages the commerce experience.
5. The CP's self-service admin tools support product, pricing, and promotions management.
6. A subscription management extension in the CP provides a self-service UI for the customer.
7. Digital River provides fraud, tax, payment, and legal compliance services via headless APIs that are embedded in the CP.
8. Subscription renewals leverage Digital River's payment optimization services to maximize renewal rates.
9. Client physical fulfillment and services provisioning systems receive and process orders.
10. Client accounting and finance systems receive remittance details from Digital River via reports, APIs, and Digital River Dashboard.
