---
description: Learn how to configure the shipping address screen.
---

# Configure the shipping address screen

1. Double click the **Shipping Address Screen** to open the Edit Screen.
2. Type `drb2b_drUtil` in the **Search components** field and click **drb2b\_drUtil**.\
   ![](<../../../../.gitbook/assets/Search drb2b\_drUtil.png>)
3. Drag the **drb2b\_drUtil** pane to where you want it to appear on the Edit Screen. \
   ![](<../../../../.gitbook/assets/Edit Screen drb2b\_drUtil.png>)
4. Type the API name (for example, `drUtil`) in the **API Name** field.\
   ![](<../../../../.gitbook/assets/Edit Screen API Name.png>)
5. Type `drb2b_buyerInfo` in the **Search components** field and click **drb2b\_buyerInfo**.\
   ![](<../../../../.gitbook/assets/Search drb2b\_buyerInfo.png>)
6. Drag the **drb2b\_buyerInfo** to where you want it to appear on the Edit Screen.\
   ![](<../../../../.gitbook/assets/Edit Screen drb2B\_buyerInfo.png>)
7.  Enter the following values in the fields:&#x20;

    * **API Name**: Type `BuyerInfo` or any other name with no restrictions.
    * **Cart Id**: Type `{!cartId}`.
    * **Enable Tax Certificates**: Type `{!$GlobalConstant.True}` or`{!$GlobalConstant.False}`.
    * **Shipping Address ID**: Type `{!contactPointAddressId}`.\
      ``**Note**: The **Shipping Address ID** field appears in the **Advanced** section when you select the **Manually assign variables** check box.

    See [Buyer info component](../../../../extend-the-salesforce-lightning-app/customizing-the-lightning-web-components/components/buyer-info-component.md) for more information.\
    ![](<../../../../.gitbook/assets/Edit Screen drb2b\_buyerInfo settings.png>)&#x20;
8. Type `drb2b_taxCertificateCheckout` in the **Search components** field and click **drb2b\_taxCertificateCheckout**.\
   ![](<../../../../.gitbook/assets/Search drb2b\_taxCertificateCheckout.png>)
9. Drag the **drb2b\_taxCertificateCheckout** to where you want it to appear on the Edit Screen.\
   ![](<../../../../.gitbook/assets/Edit Screen drb2b\_taxCertificateCheckout.png>)
10. Enter the following values in the fields:
    * **API Name**: `TaxCertificate` or any other name with no restrictions.
11. Click **Done**.&#x20;
12. Click **Save As**. \
    ![](<../../../../.gitbook/assets/Shipping Address Subflow.png>)&#x20;
13. Enter the name of the custom subflow in the **Flow Label** field (for example, DR Shipping Address) and the subfIow API name in the **Flow API Name** field, and click **Save**. \
    ![](<../../../../.gitbook/assets/Save as new flow.png>)&#x20;
14. Click **Activate**.
