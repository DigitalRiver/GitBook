---
description: >-
  Learn how to configure the Digital River settings from the Magento Admin
  Panel.
---

# Step 2: Configure the Digital River admin settings

## Step 2a: Configure general settings

1. From the **Magento Admin Panel**, select **Stores**, select **Conﬁguration**, select **Digital River Settings**, and then click **General Settings**.&#x20;
2. Click **Configuration** to expand it and complete the following fields:
   * **Enabled** – Select **Yes**. By selecting **Yes**, you are electing to include all Digital River payments enabled in the **Other Payment Methods** section on the store checkout, and for all transactions to be sent and processed by Digital River per your contract. You must select **Yes** to use the Digital River extension.
   * **Public Key** – Enter the public API key provided by Digital River.
   * **Secret Key** – Enter the secret key provided by Digital River.
   * **Enable debug logging** – By selecting **Yes**, extension errors will log debugging data.
   * **Disable automatic redirects** – Disable URL redirection_._ This setting applies to payment methods that redirect the shopper from the checkout to a page hosted by the payment instrument (for example,  Klarna, TreviPay, Direct Debit, and Online Banking). You can improve a customer's shopping experience in cases when it is required to redirect them out of the checkout flow in order to complete their transaction. Refer to [Understand redirects on the Payment page](step-4-configure-the-payment-method-settings.md) for more information. <mark style="color:red;"></mark>&#x20;
   * **Static message** – Enter the message you want to be displayed on invoice and credit memo pages created by Magento Admin Panel. &#x20;
   * **Default Selling Entity** – Type the name of the appropriate [selling entity](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/selling-entities) provided by your Digital River representative. Digital River requires a shopper address in order to determine the correct store entity to select the correct compliance links to display on the checkout page. In cases when a customer address is not yet known, you can specify the Default Selling Entity that will be used for determining the correct compliance links. Use `DR_INC-ENTITY` if you are unsure what to use or contact Digital River customer support for assistance.

## Step 2b: Configure catalog sync settings

1. Click **Catalog Sync Settings** to expand it and complete the fields:
   * **Catalog Sync Enabled**–Select **Yes**. By selecting **Yes**, you are electing to sync your Magento catalog with the Digital River SKU Service. Ensure you have cron jobs set up and configured.
   * **Start Time**–Set a time of day (hour:minute:second) for the sync to occur.
   * **Frequency**–Set a frequency (Daily:Weekly:Monthly) for the sync to run.
   * **Error Email Sender**–This is the email address from which the error notification email will be sent.
   * **Error Email Template**–Choose your email template. \
     **Note**: The default Catalog Sync Template contains file-level data that may not be included in other templates.
   * **Enable Debug Mode**–By selecting **Yes**, catalog syncing errors will log debugging data.
   * **Error Log File Name**–The file name for the error log file.
   * **Error Notification Via Email**–By selecting **Yes**, an email will be sent when there is an error in the catalog sync job.
   * **Notification Email Address**–Email address to which notifications will be sent.
   * **Catalog Batch Size Sync Limit**–The number of files that will sync with each sync job. The default is 250.

## Step 2c: Configure stored payment methods

1. Click Stored Payment Methods to expand it and complete the following fields:&#x20;
   * **Enable** – Select **Yes** or **No**. By selecting **Yes**, you are electing to allow shoppers to store their payment methods for later use.
2. Click **Save Config** when you are finished.
