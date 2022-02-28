---
description: Learn how to manage permission sets.
---

# Step 13: Manage permission sets

Assign the following Digital River permission sets to yourself or applicable users:

* **DRB2B Fulfillment Permission Set**–This permission set is required for fulfillments. Assign the [Fulfillment Integration User](step-8-set-up-digital-river-fulfillments.md#step-7b-create-a-profile) to this permission set.
* **DRB2B Permission Set**–Allows you to upsert CC Cart, CC Order, CC Transaction Payment, CC Invoice, CC Cart Item, and CC Stored Payment objects. Assign all storefront users who will place an order from the storefront to this permission set.
* **DR2B Refund Permission Set**–Allows Service Representatives to request refunds. Assign users who will [initiate refunds](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MRazfhnbBY5nfyqbUlx/v/2.0/appendix/issuing-refunds) (such as Service Representatives) to the DRB2B Refund Permission Set.

{% hint style="info" %}
**Note:** It is recommended to automate adding all storefront users to the DRB2B Permission Set.
{% endhint %}

To assign users to a permission set:

1. Type `permission sets` in the **Quick Find** field and press **Enter**. \
   ![](../.gitbook/assets/install-dr-b2b-api-connector82.png)
2. Click **Permission Sets**. The Permission Sets page appears. ![](../.gitbook/assets/install-dr-b2b-api-connector83.png)
3. Under the **Permission Set Label** column, click the permission set you want to add users to. This example shows assigning **DRB2B Permission Set** to users. \
   ![](../.gitbook/assets/install-dr-b2b-api-connector84.png)
4. From the Permission Set page, click **Manage Assignments**. ![](../.gitbook/assets/install-dr-b2b-api-connector85.png)
5. Click **Add Assignments**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector86.png>)
6. Select one or more users who you want to assign to this permission set and click **Assign**.\
   &#x20;![](<../.gitbook/assets/install-dr-b2b-api-connector87 (1).png>)\
   The assigned users now appear in the modified permission set.
