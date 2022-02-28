---
description: Learn how to configure the Checkout Summary subflow
---

# Configure the Checkout Summary subflow

## Configure a variable for the saved tax identifier

Use the variable to display saved tax identifiers.&#x20;

To create a variable:

1. Click **Setup** ![](../../../.gitbook/assets/Setup.png).
2. Type `Flows` in the **Quick Find** field click **Flows**. \
   ![](<../../../.gitbook/assets/Quick Find - Flows.png>)
3. Scroll down and click **Subflow - Checkout Summary**. The Flow Builder opens in a separate tab.\
   ![](<../../../.gitbook/assets/Flows - Subflow - Checkout Summary (2).png>)&#x20;
4. Click the **Manager** tab and then click **New Resource**. \
   ![](<../../../.gitbook/assets/Manager tab.png>)&#x20;
5. Enter the following details:
   * Select **Variable** from the **Resource Type** dropdown list.
   * **API Name**: Type `Saved_Tax_Identifier` (or any other name with no restrictions).
   * Select **Text** from the **Data Type** dropdown list.
   * Select the **Available for input** and **Available for output** check boxes.![](<../../../.gitbook/assets/New Resource.png>)
6. Click **Done**. &#x20;

{% hint style="info" %}
You can this variable to display the tax identifier when you[`configure the Checkout Summary subflow`](configure-the-checkout-summary-subflow.md#configure-the-checkout-summary-subflow).&#x20;
{% endhint %}

## Configure the Checkout Summary subflow

Use the Checkout Summary subflow to add support for US tax certificates and tax identifiers. To add custom components to  the Checkout Summary subflow:

1. From the **Manager** tab, double-click the **Cart to Order Summary** screen. &#x20;
2. Delete all OOTB components from the subflow except the **Ship To** and **Delivery Method** components.
3. Type `drb2b_drUtil` in the **Search components** field and click **drb2b\_drUtil**.\
   ![](../../../.gitbook/assets/Search-drb2b\_drUtil.png)
4. Drag the **drb2b\_drUtil** to where you want it to appear on the Edit Screen.
5. Type `drb2b_drUtil` in the **API Name** field. \
   ![](<../../../.gitbook/assets/API Name drb2b\_drUtil.png>)&#x20;
6. Type `drb2b_taxIdentifier` in the **Search components** field and click **drb2b\_taxIdentifier**.\
   ![](../../../.gitbook/assets/Search-drb2b\_taxIdentifier.png)
7. Drag the **drb2b\_taxIdentifier** to where you want it to appear on the Edit Screen.
8. Enter the following details:
   * **API Name**: Type `Tax_Identifier` (or any other name with no restrictions).
   * **Cart Id**: Type `{!cartId}`.
   * **Selected Tax Identifier**: Type `{!Saved_Tax_Identifier}`.
   * Click **Advanced**, select the **Manually assigned variables** check box, and type `{!Saved_Tax_Identifier}` in the **Selected Tax Identifier** field.![](../../../.gitbook/assets/drb2b\_taxIdentifier.png)
9. Type `drb2b_drTermsElement` in the **Search components** field and click **drb2b\_drTermsElement**.\
   ![](../../../.gitbook/assets/Search-drb2b\_drTermsElement.png)
10. Drag the **drb2b\_drTermsElement** to where you want it to appear on the Edit Screen.
11. Enter the following details:
    * **API Name**: Type `DR_Terms` (or any other name with no restrictions).
    * **Cart Id**: Type `{!cartId}`.
    * **Bypass Validation**: Type `{!$GlobalConstant.True}` or`{!$GlobalConstant.False}`. By default, this value should be `False`. See [DR terms component](../../../extend-the-salesforce-lightning-app/customizing-the-lightning-web-components/components/dr-terms-component.md) for more information.\
      ![](../../../.gitbook/assets/drb2b\_drTermsElement.png)
12. Click **Done**.
13. Click **Save as**.
14. Enter the name of the custom subflow in the **Flow Label** field (for example, `DR Checkout Summary`) and click **Save**. \
    ![](<../../../.gitbook/assets/Save as a new flow DR Checkout Summary.png>)
15. Click **Activate**. \
    ![](<../../../.gitbook/assets/Cart to  Order Summary layout.png>)&#x20;
