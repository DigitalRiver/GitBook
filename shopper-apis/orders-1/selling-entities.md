---
description: Learn how Digital River dynamically assigns selling entities.
---

# Selling entities

&#x20;As the [authorized reseller](../../#working-with-digital-river) of your products and services, Digital River sells through multiple local entities. These selling entities allow us to support localized payment processing, payment methods, and fulfillment.

The selling entity determines your [eligible payment methods](../../payments/payments-solutions/digitalriver.js/payment-methods/) and payment processors. It also determines the tax applied to the order and any [tax identifiers](../cart/configuring-taxes/managing-tax-identifiers.md) or certificates that should be collected from the customer.&#x20;

We also assign a buying entity that purchases products from you. This entity does not affect the order but does determine which Digital River entity makes a payout to you.

## How selling entities are assigned

Commerce API dynamically assigns a selling entity based on whether:

* **The country is Great Britain or the Isle of Man**–Digital River United Kingdom Ltd. is assigned to the order.&#x20;
* **The order is assigned to a fixed entity**–An order is assigned to a fixed selling entity (such as Digital River Brazil or DR Japan) that is associated with a specific site ID and locale combination. When a shopper places an order on this site, the selling entity used is based on the site's ID and locale.
* **The site is configured to use Digital River globalTech, Inc.**–If the site is configured to use DR globalTech, Inc., and the shopper is located in the United States and Canada, the selling entity is DR globalTech, Inc.&#x20;
* **The shopper using the site resides in the United States**–If the shopper resides in the United States and the site does not have a fixed entity and is not configured to use Digital River globalTech, Inc.,  the order will use the Digital River globalTech, Inc. selling entity.
* **Digital River Ireland Ltd. is assigned to the order**–If the order does not apply to any of the conditions listed above, Digital River Ireland Ltd. is assigned to the order.

The following flowchart shows how Commerce API dynamically assigns selling entities:

![](<../../.gitbook/assets/API flowchart example (1).png>)

The following table lists the selling entities associated with Commerce API.

| Selling Entity Legal Name         | Buying Entity Legal Name          |
| --------------------------------- | --------------------------------- |
| Digital River, Inc.               | Digital River, Inc.               |
| Digital River globalTech, Inc.    | Digital River globalTech, Inc.    |
| Digital River Ireland Ltd.        | Digital River Ireland Ltd.        |
| Digital River Brazil              | Digital River Brazil              |
| Digital River Japan               | Digital River Japan               |
| Digital River United Kingdom Ltd. | Digital River United Kingdom Ltd. |
