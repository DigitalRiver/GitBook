---
description: Learn how to use wire transfers to refund orders.
---

# Use wire transfers for order refunds

With the extension, you can refund order payments using wire transfers. This is done using the Credit Memo feature in the Adobe Commerce Admin UI.&#x20;

### Configure wire transfer refund method

Initiate this type of refund by using the Credit Memo feature in the Adobe Commerce Admin UI – just as you would for orders paid with any other payment method.&#x20;

When starting the refund process, you see a note advising that the refund cannot be processed until you have provided the needed bank details.

![](<../../.gitbook/assets/wiretransferrefund\_1 (2).png>)

To complete the refund process with the Credit Memo:

1. Look up the order you want to refund on the storefront, either on your **My Account** page (for authenticated shoppers) or the **Order Lookup** page (for guest shoppers).&#x20;
2. On the **Refunds** tab for your order, you are provided with a link to **Provide information** that Digital River needs to complete the refund. \
   \
   ![](../../.gitbook/assets/wiretransferrefund\_2\_order\_no.png)\

3. Click **Provide information** to open an overlay module (with secure .js fields) that lets you enter and submit your bank information.\
   \
   ![](../../.gitbook/assets/wiretransferrefund\_3\_bank\_info.png)\

4. Fill in the bank information as requested.
5. Click **Submit**. Once this information is received by Digital River, the refund will be processed.

{% hint style="info" %}
**Note:** It may take up to 3 minutes for the **Provide information** link to appear. Additionally, when the `refund.pending_information` webhook is received, it triggers a `refund_pending_information` event in Adobe. You can use this event to trigger an email to be sent to shoppers to let them know they need to provide additional information in order to process the order refund.
{% endhint %}
