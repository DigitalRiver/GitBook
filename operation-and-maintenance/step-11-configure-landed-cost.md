---
description: Learn how to configure landed cost.
---

# Step 12: Configure landed cost

Landed cost represents the total amount your customer must pay to purchase a product from one country and have it shipped to another country. It usually refers to the cost of international shipping, plus relevant taxes, duties, and fees. The Digital River landed cost feature helps customers by presenting the full cost of international orders during the time of checkout, thereby minimizing both customs delays and unanticipated expenses at the time of delivery.

After configuration, landed cost is calculated on orders where physical products are shipped across international borders to an approved country. The exception is the European Union, where shipments between countries are exempt from duties. Talk to your Digital River Business Development Manager if you need the landed cost feature to be enabled.

#### Prerequisites for the landed cost to show up in the order

* Digital River has enabled landed costs on the client account.
* Digital River has enabled the applicable trading pattern (Ship To and Ship From countries) used in the transaction.
* You, the client, have added Harmonized System (HS) Codes for all the SKUs used in the transaction.

Populate the `DR HS Code` on Products in Salesforce and run the [Product Sync](step-7.-update-the-product-sync-settings.md#product-synchronization) again.

![](<../.gitbook/assets/Populate HS code.jpg>)
