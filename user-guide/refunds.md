---
description: Learn more about refunds.
---

# Refunds

Refunds at the [Order **** ](../integrate-the-salesforce-lightning-app/step-5-add-custom-fields-to-the-page-layouts.md)and Line Item level are handled by Digital River's [Dashboard](https://dashboard.digitalriver.com/login). The Salesforce Lightning app provides a `Refunds` button on the order. Clicking the **Refunds** button will redirect the user to the **Order** details page in the Dashboard. Detailed steps on [initiating refunds](refunds.md#initiate-refunds) are featured below.

## Initiate refunds

To initiate a refund:

1. Go to the **Order** record for the completed fulfillment (that is, the **Digital River Order State** field on the order is marked **Complete**).
2. Click the dropdown menu and select **Refunds**. \
   ![](<../.gitbook/assets/Refunds 2.png>)&#x20;
3.  Click **Proceed**. You will be redirected to the **Digital River Order** page on the Dashboard.

    &#x20;![](<../.gitbook/assets/Refunds 3.png>)&#x20;
4. Click [Create refund](https://docs.digitalriver.com/digital-river-api/administration/dashboard/order-management/orders/creating-a-refund) to initiate a refund.\
   The following refund options are available:
   * Complete Order
   * Line Items
   * Shipping
   * Importer Duty
   * Importer Tax
   * Tax
5. Select your refund option and click **Review and Submit**. \
   ![](<../.gitbook/assets/Refunds 5.png>)&#x20;
6. Click **Submit**. Once the refund is initiated, the record is created in the **Refund** section of the Dashboard. \
   ![](<../.gitbook/assets/Refunds 6.png>)&#x20;

{% hint style="info" %}
You must add service representatives to the permission set, **DigitalRiver Connector – Refunds**, before making a refund request.&#x20;

Refunds can only be made for Orders that are already fulfilled.
{% endhint %}
