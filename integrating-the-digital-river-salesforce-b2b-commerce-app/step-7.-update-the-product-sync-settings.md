---
description: Learn how to update the Product Sync settings.
---

# Step 7. Update the Product Sync settings

The Product Sync page allows you to configure the behavior of the automated product synchronization. A batch job performs the synchronization, and you can schedule it to run periodically.

{% hint style="warning" %}
Set up the products you want to sync with Digital River before you perform this step. See [Step 6d: Assign tax and ECCNs to products](step-6-import-eccn-codes-tax-groups-and-tax-types.md#step-5d-assign-tax-and-eccns-to-products) for instructions.
{% endhint %}

To update the Product Sync settings:

1. Click **App Launcher** ![](<../.gitbook/assets/applauncher (4) (3).png>) .
2. Type `Digital River App` in the **Search apps and items** field. \
   ![](<../.gitbook/assets/install-dr-b2b-api-connector65 (2).png>)
3. Click **Digital River App**.
4. Click the **Product Sync** tab. \
   ![](<../.gitbook/assets/Install DR B2B API Connector37.jpg>)
5. Complete the following fields:
   * **Batch Schedule Time:** Defines the frequency of the batch job run in minutes.
   * **Batch Size**: This is the number of CC product records that the job will push to Digital River each time you run the job.
   * **Filter By Status**: By default, all CC products with a Released status will be synced to Digital River. Add a comma-separated list of CC Product statuses to override this behavior.
6. Click **Save**.
7. Click **Test DR Connection** to verify whether you can successfully connect with the configured Digital River site. If there are errors, check your settings and try again.
8. Click **Sync All** to sync all the CC products for which DR ECCN, DR TaxGroup, and DR TaxType fields are populated.
9. Click **Re-sync All** to sync CC Products for which **Sync Product to DR** flag is set to **true**. This flag gets set to true whenever relevant fields on the CC Product have been modified.
