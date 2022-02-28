---
description: Learn how to use the Product MetaFields module.
---

# Product Meta Fields module

The WooCommerce plugin includes the `ProductMetaFields` under the **Digital River** tab.

To access the product meta fields when creating a product under **Product Data**, click the **Digital River** tab, and enter the **ECCN, Country of Origin, Tax Code** (it will change according to product type), and [HS Code](https://www.trade.gov/harmonized-system-hs-codes) **** (optional). See [how to create a product](https://docs.woocommerce.com/document/managing-products/#section-6?) for more information.

![](<../../.gitbook/assets/Product-Meta-Fields-Digital-River-Tab (2).png>)

{% hint style="info" %}
When creating a product, the **SKU** field under the **Inventory** tab is mandatory.
{% endhint %}

Once the product is published, it will be auto-synced to Digital River. You can always resync from the product edit screen only, in case the product sync is failed. Clicking **Sync Product** will sync the product.

![](<../../.gitbook/assets/Sync-to-Digital-River (1).png>)

Once the product is synced, check under API logs in [Digital River Dashboard](https://dashboard.digitalriver.com/login). The log is identified by SKU for product sync. \
&#x20;&#x20;

![](<../../.gitbook/assets/Synced=Product-in-Digital-River-Dashboard (1).png>)
