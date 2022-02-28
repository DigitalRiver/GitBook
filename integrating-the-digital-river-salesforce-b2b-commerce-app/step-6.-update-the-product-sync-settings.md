---
description: Learn how to update the Product Sync settings.
---

# Step 6. Update the Product Sync settings

The Product Sync page allows you to configure the behavior of the automated product synchronization. A Batch job performs the synchronization, and you can schedule it to run periodically.

{% hint style="warning" %}
Set up the products you want to sync with Digital River before you perform this step. See [Step 5d: Assign tax and ECCNs to products](step-5-import-eccn-codes-tax-groups-and-tax-types.md#step-5d-assign-tax-and-eccns-to-products) for instructions.
{% endhint %}

To update the Product Sync settings:

1. Click **App Launcher** ![](../.gitbook/assets/App-Launcher.png) .
2. Type `Digital River App` in the **Search apps and items** field. \
   ![](../.gitbook/assets/Search-apps-and-items.png)
3. Click **Digital River App**.
4. Click the **Product Sync** tab. \
   ![](<../.gitbook/assets/product-sync (1).png>)
5. Complete the following fields:
   * **Size**: This is the number of CC product records that the job will push to Digital River each time you run the job.
   * **Filter By Status**: By default, all products with a Released status will be synced to Digital River. Add a comma-separated list of CC Product statuses to override this behavior.
   * **Batch Schedule Time**: Defines the frequency of the batch job run in minutes.
6. Click **Test DR Connection** to verify whether you can successfully connect with the configured Digital River site.
7. If the connection to Digital River is successful, click **Save**. If there are errors, check your settings and try again.
