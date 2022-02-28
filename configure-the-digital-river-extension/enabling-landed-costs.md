---
description: Learn how to enable landed costs.
---

# Enabling landed costs

Landed costs represent the entire cost a customer must pay to purchase a product from one country and have it shipped to an address in another country. It includes product price, shipping, taxes, duties, and fees. Digital River provides an estimated landed cost for you to display to the customer and adds the cost to the order total. Digital River remits those landed costs to you. Your fulfiller relays the order to your carrier, who completes the customs paperwork, ships the package to the destination country, pays the duties and taxes on behalf of your customer, and invoices you for performing the service.

To take advantage of the landed cost feature, complete the following steps:

1. Verify your fulfiller ships packages outside their country (not all fulfillers provide this service).
2. Verify your carrier offers this service. In other words, verify the carrier prepays the landed costs on behalf of the customer and sends the invoice to you.
3. Sign an addendum in your Digital River contract to enable landed costs.
4. Define the cross-border patterns (that is, the ship-to countries) where you want to collect landed costs.
5. Provide samples of completed customs forms to Digital River's Compliance department for approval.
6. Provide your Account Manager with a list of the ship-from and ship-to countries for which you want to enable the collection of landed costs.

{% hint style="info" %}
**Note**: To prevent double taxation, set all Tax and Display settings to **Excluding Tax**.
{% endhint %}

To enable the landed cost feature, complete the following steps in the Magento Admin UI:

1. In Digital River settings, specify the HS code for each product in your Magento Catalog you plan to sell cross-border.
2. [Sync each of the products](enabling-landed-costs.md#step-2b-catalog-sync-settings) you plan to sell cross-border with the Digital River SKU Service.
3. Enter your warehouse address in the **Shipping Origin** field in your Store Configurations (Stores > Configuration > Sales > Shipping Settings > Origin) and click **Save**.

Once this feature is configured, landed costs will be calculated, collected, and applied to orders that contain physical goods that are shipped cross-border to approved countries.
