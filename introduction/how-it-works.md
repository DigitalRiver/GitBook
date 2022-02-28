---
description: Learn how the Salesforce Lightning app works.
---

# How it works

Use the Salesforce Lightning app to enable Digital River to be the merchant of record for storefronts hosted on the Salesforce platform.

* Salesforce Lightning B2B Commerce maintains all pricing and product data.
* Digital River maintains minimal product data used to fulfill its requirements as the merchant of record. This data is used for tax calculations, tax collection, tax payments, and payment processing.
* Digital River automatically syncs with the Product (Product2) in Salesforce Lightning with minimal information needed to calculate taxes and enable the merchant of record functions.
* Digital River maintains a copy of the cart (WebCart), the customer, and the order.
* The fulfiller updates the status of the order from `accepted` to `fulfilled` or `canceled` in Salesforce. The Digital River app sends the updated order status to Digital River, who will settle the funds.

## Digital River checkout flow

{% file src="../.gitbook/assets/DR_Checkout_Flow_v1.1_updated.png" %}

