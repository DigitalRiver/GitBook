---
description: Learn more about refunds.
---

# Refunds

Refunds at the [Order](../operation-and-maintenance/step-4-add-custom-salesforce-lightning-app-fields-to-page-layouts.md#order-standard-object) **** and Line Item level are handled by Digital River's [Dashboard](https://dashboard.digitalriver.com/login). The Salesforce Lightning app provides a `Refunds` button on the order. Clicking the **Refunds** button will redirect the user to the **Order** details page in the Dashboard. Detailed steps on [initiating refunds](../operation-and-maintenance/step-4-add-custom-salesforce-lightning-app-fields-to-page-layouts.md#initiate-refunds) are featured below.

## Initiate refunds

To initiate a refund:

1. Go to the **Order** record for the completed fulfillment (that is, the **Digital River Order State** field on the order is marked **Complete**).
2. Click the dropdown menu and select **Refunds**. \
   <img src="../.gitbook/assets/Refunds 2.png" alt="" data-size="original">&#x20;
3. Click **Proceed**. You will be redirected to the **Digital River Order** page on the Dashboard. <img src="../.gitbook/assets/Refunds 3.png" alt="" data-size="original">&#x20;
4. Click Create refund to initiate a refund.\
   The following refund options are available:
   * Complete Order
   * Line Items
   * Shipping
   * Importer Duty
   * Importer Tax
   * Tax
5. Select your refund option and click **Review and Submit**. \
   <img src="../.gitbook/assets/Refunds 5.png" alt="" data-size="original">&#x20;
6. Click **Submit**. Once the refund is initiated, the record is created in the **Refund** section of the Dashboard. \
   <img src="../.gitbook/assets/Refunds 6.png" alt="" data-size="original">&#x20;

{% hint style="info" %}
You must add service representatives to the permission set, **DigitalRiver Connector – Refunds**, before making a refund request.&#x20;

Refunds can only be made for Orders that are already fulfilled.
{% endhint %}
