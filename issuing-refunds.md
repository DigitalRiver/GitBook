---
description: Learn how to issue refunds through the Salesforce B2B Commerce App.
---

# Issuing refunds

The Digital River Salesforce B2B Commerce App provides customers the ability to request a full or partial refund at the order level. Currently, there is no support in the App to request a refund at the line-item level or on shipping costs, taxes, fees, and duties.

To refund for shipping costs, the Service Representative can issue a refund request at the order level and enter the shipping cost amount.

To issue refunds through the App:

1. Go to the CC Order record for which fulfillment is completed (that is, the **Digital River Order State** field on CC Order is **complete)**.
2. Click **Refund**. This Refunds page appears with CC Order Number, DR Order Id, Available Amount to Refund, and a section for Previously submitted refunds. \
   ![](<.gitbook/assets/Install DR B2B API Connector110.png>)
3. For **Refund For**, select **Full Order**.
4. For **Refund**, select the appropriate adjustment value from the dropdown list.
5. For **Reason**, select the reason for refunds from the dropdown list.
6. Specify your comments in the **Comments** text box.
7. Enter the amount to be refunded in the **Refund Amount** text box. ![](<.gitbook/assets/Install DR B2B API Connector111.png>)
8. Click **Submit Refund Request**. The refund request will be submitted to Digital River and the page will refresh. You should see this refund request information in the Previous Refunds section. You should also see that the available refund amount is now updated. \
   ![](<.gitbook/assets/Install DR B2B API Connector112.png>)

**Notes**:

* You must add Service Representatives to the DRB2B Refund Permission Set before they can make a refund request.
* Refunds can only be made for orders that are already fulfilled. Otherwise, you will see an error saying “Fulfillment is not yet done for this Order”.

![](<.gitbook/assets/Install DR B2B API Connector113.png>)
