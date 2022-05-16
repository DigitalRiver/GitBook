---
description: Learn how to configure products.
---

# Configuring products

Map all Magento Product SKUs to Digital River. You must share all your SKU values with Digital River for Digital River to conﬁgure the payment gateway. &#x20;

The API call executed for syncing products with the Digital River SKU Service is a PUT request as follows: `PUT` [`https://api.digitalriver.com/skus/24-MB01`](https://api.digitalriver.com/skus/24-MB01). Because the SKU ID is part of the URL, SKU IDs must not contain spaces or special characters.

{% hint style="info" %}
**Note**: SKU IDs should be limited to \[a-zA-Z0-9.-:\*\_]
{% endhint %}

1. Select **Catalog**, then select **Products**.&#x20;
2. Click **Edit** at the right end of the listed product you wish to edit to open a new page.&#x20;
3. Scroll down to the **Digital River** section and click to expand the section.&#x20;
   *   **ECCN Code**–From the dropdown list (which is searchable), choose the ECCN that applies to your product, which completes the Classification number and Digital River’s Description and Notes. Pay attention to the Notes, as they may contain important information relevant to your ECCN. If you do not find the ECCN applicable to your product, contact your Digital River account representative.

       [ECCN list](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn)

       [Approved ECCNs](https://help.digitalriver.com/legal/Legal.htm#ApprovedECCNs)
   * **Tax Group**–From the dropdown list, choose the Tax Group that applies to your product. The Tax Group selection will determine the Tax Type options. If you have questions, contact your Digital River account representative.
   * **Tax Type**–From the dropdown list, choose the Tax Type that applies to your product.
   * **Country of Origin**–From the dropdown list, choose the Country of Origin for your product. See this [country codes list](https://www.iso.org/iso-3166-country-codes.html).
   * **HS Code**–Enter the HS Code that applies to your product. This field is only used if you are set up to provide [landed costs](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/landed-costs) to your shoppers. If you are interested in enabling landed costs, contact your Digital River account representative.

{% hint style="info" %}
**Note:** For each product, you must deﬁne all values in the following table except HS codes before launching a live storefront. The HS codes are only required if you want to calculate landed cost. These values will be imported into the Digital River SKU Service and the data will be used to ensure proper taxation.
{% endhint %}

{% hint style="info" %}
**Additional notes**:&#x20;

* Every product sold via the Digital River Extension for Magento will be considered Taxable Goods in the Magento production conﬁguration screen.
* The tax group and tax type determine if a SKU is considered a digital or physical product in the Digital River SKU service. Incorrectly categorizing a physical product with a digital tax value can cause orders to fail.
* Each digital product must be set to **This item has no weight** within the Adobe Commerce admin settings. This setting tells the extension how to handle digital products at checkout.
{% endhint %}

## Manual catalog sync

The catalog will sync according to your Catalog Sync Settings. However, you can also sync your catalog manually. Select **Catalog**, then click **Catalog Sync Grid**, and then click **Manual Sync To Digital River**.

## Catalog sync error handling

Based on the response from Digital River, the individual records in the `dr_sync_queue` will be updated as follows:

### On success

1. The `synced_to_dr_at` will be updated with the timestamp in the response field **updatedTime**.
2. The status will be updated to **Success**.
3. `Response_data` will be updated with the response received from Digital River.

#### On failure

1. The `synced_to_dr_at` will be updated with the timestamp in the response field **updatedTime**.
2. The status will be updated to **Fail** or **Pending**, depending on the error response code as listed below, and the Failure Response JSON node will be logged in the `response_data` column for tracking purposes.
   * For the **500 error**, the status will be left **Pending** so that the next time the scheduler starts it will try again to sync the data.
   * For the **400 error**, the status will be updated to **Fail**.
3. The merchant must update the product data based on the error response against that queue row.  When the merchant updates the data from **Admin**, the product will again get added in the queue with the status **Pending** and will get synched to Digital River.
4. If there is a failure during the sync, even for a single record, then take note at the end of the sync process and try one of these adjustments, depending on the cause of failure:
   * Update the product to resolve the error.&#x20;
   * Retry the sync.
