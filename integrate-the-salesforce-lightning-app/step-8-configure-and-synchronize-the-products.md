---
description: Learn how to configure and synchronize the products.
---

# Step 8: Configure and synchronize the products

Product management consists of two aspects. First, the required product attributes must be configured for each product/SKU. Next, the products must be synced to Digital River. This section includes [product configuration](step-8-configure-and-synchronize-the-products.md#product-configuration) and [product synchronization](step-8-configure-and-synchronize-the-products.md#product-synchronization).

## Configure product attributes

For each product or SKU, you must configure the [product attributes](step-5-add-custom-fields-to-the-page-layouts.md) to send to Digital River.

In the **Product** tab, the tax code object will map to the **DR TAXGROUP** and **DR TYPE** in the **Digital River Tax Mappings** field. The **ECCN code** maps to the **Digital River ECCN code** object.&#x20;

![](<../.gitbook/assets/Product setup and sync.png>)

When a Digital River field is changed, it is marked for synchronization. When a product synchronization batch job runs, any products marked for synchronization should be synced.

![](<../.gitbook/assets/Digital River tax mapping custom object.png>)

### DR Product Country Origin (Picklist)

{% hint style="warning" %}
Within the Salesforce Lightning app installation, **Country Names** and corresponding **Country ISO codes** will come pre-populated on the custom field **DR Product Country Origin** on the **Product** object.

Any changes (additions, deletions, or modifications) to these picklists must be done manually after installation.
{% endhint %}

## Configure product synchronization

The **Product Sync** tab allows you to configure the behavior of the automated product synchronization. A batch job performs the synchronization, and you can schedule it to run periodically.

{% hint style="warning" %}
Products missing any required fields (for example, DR Product Country Origin, DR TAXGROUP, DR TAXTYPE, and DR ECCN) will not be synced to Digital River. Digital River uses this information to [calculate tax](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/tax-calculations).&#x20;
{% endhint %}

To update the **Product Sync** settings:

1. Click the App Launcher ![](<../.gitbook/assets/App launcher.png>).
2. Type **Digital River App** in the **Search apps and items** field and click **Digital River App**.\
   &#x20;![](<../.gitbook/assets/DR App in Search.png>)&#x20;
3. Click the **Product Sync** tab. \
   ![](<../.gitbook/assets/Product Sync tab.png>)&#x20;
4. Complete the following fields:
   * **Batch Schedule Time**: Defines the frequency of the batch job run in minutes.
   * **Batch Size**: The number of Salesforce product records that the job will push to Digital River each time you run the job.
5. Click **Save**.
6. Click **Sync products** (to sync the products).
7. Click **Re-Sync All Products** (to resync all products).&#x20;



