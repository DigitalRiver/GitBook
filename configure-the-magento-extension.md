---
description: Learn how to configure the Digital River Extension.
---

# Configure the Digital River Extension

A Digital River account is required to use this extension. If you do not have a Digital River account, you can sign up for one [here](https://dashboard.digitalriver.com/signup).

Below are the steps for configuring this extension:

* [Step 1: Retrieve API credentials from the Digital River Dashboard](configure-the-magento-extension.md#step-1-retrieve-api-credentials-from-the-digital-river-dashboard)
* [Step 2: Configure the Digital River admin settings in Magento](configure-the-magento-extension.md#step-2-configure-the-digital-river-admin-settings-in-magento)
* [Step 3: Create a webhook](configure-the-magento-extension.md#step-3-create-a-webhook)
* [Step 4: Configure the payment method settings](configure-the-magento-extension.md#step-4-configure-the-payment-method-settings)
* [Step 5: Configure other store settings in Magento](configure-the-magento-extension.md#step-5-configure-other-store-settings-in-magento)

## Step 1: Retrieve API credentials from the Digital River Dashboard

The Digital River Dashboard is your portal to your Digital River account. You can use [Dashboard](https://dashboard.digitalriver.com/login) to retrieve your API keys, view Payouts, or search API logs.&#x20;

1. Sign in to [Dashboard](https://dashboard.digitalriver.com/login).&#x20;
2. On the **API keys** page, make note of the **Standard keys** and **Restricted keys**. \
   You will use these keys in[ Step 2](configure-the-magento-extension.md#step-2-configure-the-digital-river-admin-settings-in-magento). See [Getting your API keys](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/api-keys) in the Dashboard documentation for instructions on retrieving your API credentials. &#x20;

![](<.gitbook/assets/APIKeysNew (1).png>)

## Step 2: Configure the Digital River admin settings in Magento

### Step 2a: Configure general settings

1. From the **Magento Admin Panel**, select **Stores**, select **Conﬁguration**, select **Digital River Settings**, and then click **General Settings**.
2.  Click **Configuration** to expand it and complete the following fields:

    | Settings             | Description                                                                                                                                                                                                                                                |
    | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Enabled              | Select **Yes**. By selecting **Yes**, you are electing to include all Digital River payments enabled in the **Other Payment Methods** section on the store checkout, and for all transactions to be sent and processed by Digital River per your contract. |
    | Public Key           | Enter the public API key provided by Digital River.                                                                                                                                                                                                        |
    | Secret Key           | Enter the secret key provided by Digital River.                                                                                                                                                                                                            |
    | Signing Secret       | Enter the signing secret provided by Digital River.                                                                                                                                                                                                        |
    | Enable debug logging | By selecting **Yes**, extension errors will log debugging data.                                                                                                                                                                                            |

### Step 2b: Catalog sync settings

1.  Click **Catalog Sync Settings** to expand it and complete the fields:

    | Settings                      | Description                                                                                                                                                              |
    | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | Catalog Sync Enabled          | Select **Yes**. By selecting **Yes**, you are electing to sync your Magento catalog with the Digital River SKU Service. Ensure you have cron jobs set up and configured. |
    | Start Time                    | Set a time of day (hour:minute:second) for the sync to occur.                                                                                                            |
    | Frequency                     | Set a frequency (Daily:Weekly:Monthly) for the sync to run.                                                                                                              |
    | Error Email Sender            | This is the email address from which the error notification email will be sent.                                                                                          |
    | Error Email Template          | <p>Choose your email template. <br><strong>Note</strong>: The default Catalog Sync Template contains file-level data that may not be included in other templates.</p>    |
    | Enable Debug Mode             | By selecting **Yes**, catalog syncing errors will log debugging data.                                                                                                    |
    | Error Log File Name           | The file name for the error log file.                                                                                                                                    |
    | Error Notification Via Email  | By selecting **Yes**, an email will be sent when there is an error in the catalog sync job.                                                                              |
    | Notification Email Address    | Email address to which notifications will be sent.                                                                                                                       |
    | Catalog Batch Size Sync Limit | The number of files that will sync with each sync job. The default is 250.                                                                                               |
2. Click **Save Conﬁg** when you are ﬁnished.

## Step 3: Create a webhook

You create webhooks to receive integration messages from Digital River. Those messages are triggered by events in Digital River’s application. When triggered, the event messaging will update the Adobe Commerce (Magento) order status (see [Exhibit B](appendix-1.md#exhibit-b-sequence-diagram) in the Appendix section). &#x20;

Create a webhook to receive notifications using the following steps:

* Step 3a: Open your firewall to trusted Digital River IP addresses
* Step 3b: Create a webhook endpoint
* Step 3c: Create webhooks

### Step 3a: Open your firewall to trusted Digital River IP addresses

To receive webhook notifications from Digital River, you will need to open your firewall to all the IP addresses listed in the [Digital River safelist](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/webhooks/digital-river-safelist).

### Step 3b: Create a webhook endpoint

You can send webhook data as JSON in the POST request body. The POST request body contains the complete event details, and you can use it after parsing the JSON into an [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object.

Your webhook endpoint URL should be the URL to your Magento installation + `drpay/receive` \
**Example**: `https://exmage.drgc.shop/drpay/receive`

### Step 3c: Create webhooks&#x20;

When creating webhooks, you need to add endpoints from the [Dashboard](https://dashboard.digitalriver.com):

1. From the **Webhooks** page, click **Create Webhook**.
2. Toggle **Disabled** to **Enabled**.
3. If required, select the API version you want to associate with events from the **API Version** dropdown list. By default, the confidential key version is selected.
4. Enter the URL for the endpoint in the **Endpoint URL** field.
5. Select the check box next to each event you want to associate with the endpoint or select the **Events Selected** check box to select all events. At least one event type must be selected.
6. Scroll down and click **Save**.\
   &#x20;![](.gitbook/assets/CreateWebhook.png)&#x20;

Webhooks must be created for the following events:

* `order.accepted`
* `order.complete`
* `order.blocked`
* `refund.failed`
* `order.review_opened`
* `order.invoice.created`
* `order.credit_memo.created`
* `refund.failed`
* `order.charge.refund.complete`
* `order.charge.refund.failed`

## Step 4: Configure the payment method settings

Since Digital River acts as the merchant of record on all transactions, payment methods must be configured by Digital River. Work with your Digital River representative to configure the selection and display of payment methods in the Digital River Drop-in payment integration. Enabling Digital River payment methods and other payment methods on the configuration page for the same store will result in failures.

1. From the **Magento Admin panel**, select **Stores**, select **Conﬁguration**, select **Sales**, select **Payment Methods**.
2. In **Payment Methods**, make the following selections:
   * Select **Check/Money Order**. Then set **Enabled** to **No**.
   * Select **Cash On Delivery Payment**. Then set **Enabled** to **No**.
   * Select **Bank Transfer Payment**. Then set **Enabled** to **No**.
   * Select **Purchase Order**. Then set **Enabled** to **No**.
   * Select **Digital River Payment**. Then set **Enabled** to **Yes**.

## Step 5: Configure other store settings in Magento

Make the following selections to configure other store settings:

1. From the **Magento Admin panel**, select **Stores**, then select **Conﬁguration.**
2. In **Configuration**, select **General**, and then select **Store Information**. By default, your store address will be used as your ship from address for all transactions.
3. Select **Sales**, and then select **Multishipping Settings**. Then click **No** for **Allow Shipping to Multiple Addresses**.

## Configuring taxes

The Digital River Global Commerce version 2.2.0 Extension for Adobe Commerce is responsible for providing the end tax calculation for the shopper navigating the checkout. The extension supports both tax-inclusive and tax-exclusive pricing models and handles all remittance and tax liabilities to local governments globally. The transactional tax is not calculated until after the shopper conﬁrms their billing and shipping address. Digital River does not support or allow the display of tax calculations that are not provided by Digital River. To ensure estimated tax and tax display is consistent throughout the pre-checkout pages, Digital River recommends the following conﬁgurations for tax, based on pricing models.

{% hint style="info" %}
**Note**: Each Magento website or store should be tax-exclusive or tax-inclusive for all products and shipping. One store should not use both or a mixture of inclusive and exclusive pricing.&#x20;

**Note**: The Digital River Extension for Magento cannot be used with other Magento tax partners.
{% endhint %}

### Tax settings

To ensure the correct display of taxes in all situations, conﬁgure your Magento tax settings as follows:

1. Select **Stores**, select **Conﬁguration**, select **Sales**, and then click **Tax**.&#x20;
2. In the **Tax Classes** section, update **Tax Class for Shipping** to **Taxable Goods**.\
   &#x20;![](.gitbook/assets/8TaxClassShipping.png)&#x20;
3. In the **Shopping Cart Display Settings**, keep the **Display Full Tax Summary** set to **No**.\
   &#x20;![](.gitbook/assets/9DisplayFullTax.png)&#x20;

#### Tax exclusive settings

To display tax exclusive values in your catalog, order summary, and checkout, configure your settings as follows:

1. Select **Stores**, select **Conﬁguration**, select **Sales**, select **Tax**, and then click **Calculation Settings**.
2. Verify **Catalog Prices** is set to `Excluding Tax` —this is the default setting.\
   &#x20;![](.gitbook/assets/10CatalogPrices.png)&#x20;
3. On the same **Tax** page, click to expand the **Price Display Settings** section, the **Shopping Cart Display Settings** section, and the **Orders**, **Invoices**, **Credit Memos Display Settings** section. In each section, verify the following are also conﬁgured for `Excluding Tax`—these are the default settings.\
   &#x20;![](.gitbook/assets/11PriceDisplaySettings.png)&#x20;
4. All prices in the catalog must be exclusive of tax.

### Tax Inclusive settings

To display tax inclusive values in your catalog, order summary, and checkout, configure your settings as follows:

1. Select **Stores**, select **Conﬁguration**, select **Sales**, select **Tax**, and then click **Calculation Settings**.\
   &#x20;![](.gitbook/assets/13PriceDisplaySettings.png)&#x20;
2. Click the **Catalog Prices** dropdown list and change the setting to `Including Tax`.\
   &#x20;![](.gitbook/assets/14CatalogPrices.png)&#x20;
3. On the same **Tax** page, click to expand the **Price Display Settings** section, the **Shopping Cart Display Settings** section, and the **Orders, Invoices, Credit Memos Display Settings** section. In each section, update the configuration to `Including Tax`.

## Configuring products

Map all Magento Product SKUs to Digital River. You must share all your SKU values with Digital River for Digital River to conﬁgure the payment gateway. &#x20;

The API call executed for syncing products with the Digital River SKU Service is a PUT request as follows: `PUT` [`https://api.digitalriver.com/skus/24-MB01`](https://api.digitalriver.com/skus/24-MB01). Because the SKU ID is part of the URL, SKU IDs must not contain spaces or special characters.

{% hint style="info" %}
**Note**: SKU IDs should be limited to \[a-zA-Z0-9.-:\*\_]
{% endhint %}

1. Select **Catalog**, then select **Products**.&#x20;
2. Click **Edit** at the right end of the listed product you wish to edit to open a new page.&#x20;
3. Scroll down to the **Digital River** section and click to expand the section.&#x20;

{% hint style="info" %}
**Note:** For each product, you must deﬁne the following values before launching a live storefront. These values will be imported into the Digital River SKU Service and the data will be used to ensure proper taxation.
{% endhint %}

| Name              | Action                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ECCN Code         | <p>From the dropdown list (which is searchable), choose the ECCN that applies to your product, which completes the Classification number and Digital River’s Description and Notes. Pay attention to the Notes, as they may contain important information relevant to your ECCN. If you do not find the ECCN applicable to your product, contact your Digital River account representative.</p><p><a href="https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn">ECCN list</a></p><p><a href="https://help.digitalriver.com/legal/Legal.htm#ApprovedECCNs">Approved ECCNs</a></p> |
| Tax Group         | From the dropdown list, choose the Tax Group that applies to your product. The Tax Group selection will determine the Tax Type options. If you have questions, contact your Digital River account representative.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Tax Type          | From the dropdown list, choose the Tax Type that applies to your product.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Country of Origin | From the dropdown list, choose the Country of Origin for your product. See this [country codes list](https://www.iso.org/iso-3166-country-codes.html).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| HS Code           | Enter the HS Code that applies to your product. This field is only used if you are set up to provide [landed costs](configure-the-magento-extension.md#enabling-landed-cost) to your shoppers. If you are interested in enabling landed costs, contact your Digital River account representative.                                                                                                                                                                                                                                                                                                                                                       |

{% hint style="info" %}
**Note**: Every product sold via the Digital River Extension for Magento will be considered Taxable Goods in the Magento production conﬁguration screen.
{% endhint %}

### Manual catalog sync

The catalog will sync according to your Catalog Sync Settings, however, you can also sync your catalog manually. Select **Catalog**, then click **Catalog Sync Grid**, and then click **Manual Sync To Digital River**.

### Catalog sync error handling

Based on the response from Digital River the individual records in the `dr_sync_queue` will be updated as follows:

### On success

1. The `synced_to_dr_at` will be updated with the timestamp in the response field **updatedTime**.
2. The status will be updated to **Success**.
3. `Response_data` will be updated with the response received back from Digital River.

### On failure

1. The `synced_to_dr_at` will be updated with the timestamp in the response field **updatedTime**.
2. The status will be updated to **Fail** or **Pending**, depending on the error response code as listed below, and the Failure Response JSON node will be logged in the `response_data` column for tracking purposes.
   * For the **500 error**, the status will be left **Pending** so that the next time the scheduler starts it will try again to sync the data.
   * For the **400 error**, the status will be updated to **Fail**.
3. The merchant must update the product data based on the error response against that queue row.  When the merchant updates the data from **Admin**, the product will again get added in the queue with the status **Pending** and will get synched to Digital River.
4. If there is a failure during the sync, even for a single record, then take note at the end of the sync process and try one of these adjustments, depending on the cause of failure:
   * Update the product to resolve the error.&#x20;
   * Retry the sync.

## Enabling landed cost

Landed costs represent the entire cost a customer must pay to purchase a product from one country and have it shipped to an address in another country. It includes product price, shipping, taxes, duties, and fees. Digital River provides an estimated landed cost for you to display to the customer and adds the cost to the order total. Digital River remits those landed costs to you. Your fulfiller relays the order to your carrier, who completes the customs paperwork, ships the package to the destination country, pays the duties and taxes on behalf of your customer, and invoices you for performing the service.

To take advantage of the landed cost feature, you'll need to complete the following steps:

1. Verify your fulfiller ships packages outside their country (not all fulfillers provide this service).
2. Verify your carrier offers this service. In other words, does the carrier prepay the landed costs on behalf of the customer and send the invoice to you.
3. Sign an addendum in your Digital River contract to enable landed costs.
4. Specify the `hsCode` parameter, which represents the Harmonized System code, when creating new SKUs or performing update or upsert operations on the SKUs in your catalog.
5. Define the cross-border patterns (that is, the ship-to countries) where you want to collect landed costs.
6. Provide samples of completed customs forms to Digital River's Compliance department for approval.
7. Provide your Account Manager with a list of the ship from and ship to countries for which you want to enable the collection of landed costs.
8. Once the feature is configured and set up, we calculate, collect, and apply landed costs to orders that contain physical goods and are shipped across borders to approved countries.

{% hint style="info" %}
**Note**: To prevent double taxation, all of your Tax and Display settings must be set to **Excluding Tax**.
{% endhint %}

## Terms of sale, privacy policy, and acceptance check box during checkout&#x20;

Since Digital River is the merchant of record on all transactions, our Terms of Sale, Privacy Policy, and other links must be present on checkout. No configuration is required by the client since Digital River dynamically determines the appropriate Digital River selling entity for each order and displays the appropriate language, links, and checkboxes.

![](.gitbook/assets/TermsofSale.png)

## Configuring a second website, store, or store view

The Digital River Extension for Magento is conﬁgurable by the website in the Magento Admin Panel interface. This enables administrators to offer different payment methods and different currencies to different regions.

The only ﬁeld that changes is the Base Conﬁguration locale ﬁeld. Digital River will provide the locale needed to meet your language, payment, and currency requirements. Payments are also conﬁgurable via [Drop-in](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/drop-in) by the website.

See [Set up multiple websites, stores, and store views in the Admin](https://devdocs.magento.com/guides/v2.3/config-guide/multi-site/ms\_websites.html) for additional information.

### Localizations and translations

All content displayed via the Digital River Extension can be modiﬁed by adding an `/i18n` directory to the _DrPay_ folder. By default the extension supports the following languages: \[en, es, it, fr, sv, da, ﬁ, cs, pl, hu, de, nl, pt, nl, fr] `/app/code/Digitalriver/DrPay/i18n`.&#x20;

![](.gitbook/assets/17SpreadsheetListing.png)

After translation ﬁles are added or updated, rerun the upgrade command:\
`$ php bin/magento setup:upgrade`

To ensure translated text is reﬂected on the Magento website or store view, it is important to update the locale option for that website or store view via the general Magento settings: Select **Stores**, then **Conﬁguration**, then **Genera**l, and then click **Locale Options**.

## New columns in the Magento Admin UI

Digital River's extension adds two columns to the Sales Orders grid: **DR Order ID** and **DR Payment Method**. To access the Sales Orders grid, select **Sales**, and then select **Orders** using the **Columns** dropdown.

| **Sales Orders Grid**   | Description                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DR Order ID             | <p>Lists the primary order identification number in Digital River’s systems. <br><strong>Note</strong>: The Magento Commerce ID is a secondary ID in Digital River’s systems. <img src=".gitbook/assets/DR Order ID and DR Payment Method (1).png" alt=""> </p>                                                                                                                                       |
| DR Payment Method       | <p>Replaces the standard <strong>Payment Method</strong> column. One or both can be used, however, the <strong>Payment Method</strong> column will always display <strong>DigitalRiver Payments</strong>, where the <strong>DR Payment Method</strong> will display the actual payment method used on the transaction.</p><p><img src=".gitbook/assets/DR Payment Method (1).png" alt=""> </p><p></p> |

### Saved payment methods

At this time, payment methods can only be saved to a shopper’s account during checkout. The shopper can choose to save the payment method by clicking the box named **Yes, please** **save this account and payment information for future purchases**. The saved payment method will not appear in the shopper's **My Account** pages. This functionality will be added in a future release.

![](<.gitbook/assets/Stored payment methods (6).png>)

### Store Credit&#x20;

Customers can now use Magento Store Credit to pay for all or part of an order processed by Digital River. Store Credit can be used in combination with multiple [payment methods](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/payment-sources/using-the-source-identifier#combining-primary-and-secondary-payment-sources).&#x20;

For orders paid with a combination of Store Credit and one of the other supported payment methods, the **DR Payment Method** will be listed as the non-Store Credit payment instrument (for example,  PayPal). For orders paid entirely with Store Credit, the **DR Payment Method** will be **CustomerCredit**.

![](<.gitbook/assets/Store Credit (1).png>)

#### Refunding orders paid with Store Credit

Orders paid partially or entirely with Store Credit can be refunded through the normal Magento admin screens.&#x20;

If a transaction was paid partially with Store Credit and partially with another payment method, Digital River will always refund the payment method first.&#x20;

{% hint style="info" %}
**Note**: Digital River will never refund more to any payment method than was originally paid using that payment method on the original purchase.
{% endhint %}

![](<.gitbook/assets/Refund order paid\_Store Credit (1).png>)

#### Refunding to Store Credit when order paid using another payment method

When an order has been paid without Store Credit on the initial transaction, refunding to the shopper’s store credit account must be done in accordance with _Digital River’s Guidelines and Best Practices._

Due to how Digital River processes refunds, the **Refund to Store Credit** function has been removed from the **Magento Credit Memo** page.&#x20;

The **Magento Credit Memo** page has been modified to only allow refunds to the original payment methods used on the original purchase.&#x20;

Store Credit can still be returned to the shopper’s account by adding it directly to their account from the Customer’s Admin page in the Magento Admin UI.&#x20;

![](<.gitbook/assets/Refunding to store credit (1).png>)

### Gift Cards

Customers can now use one or more Magento Gift Cards to pay for all or part of an order processed by Digital River. Gift Cards can be used in combination with multiple [payment methods](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/payment-sources/using-the-source-identifier#combining-primary-and-secondary-payment-sources).

With Store Credit, orders paid with a combination of Gift Card and one of the other supported payment methods, the **DR Payment Method** will be listed as the non-Gift Card payment instrument (for example, PayPal). For orders paid entirely with a Gift Card, the **DR Payment Method** will be **CustomerCredit**.

![](<.gitbook/assets/Gift Cards (1).png>)

#### Refunding orders paid with Gift Cards

Orders paid partially or entirely with Gift Cards can be refunded through the normal Magento admin screens.&#x20;

If a transaction was paid partially with one or more Gift Cards and partially with another payment method, Digital River will always refund to the other payment method first until that payment method has been refunded the entire amount paid using that payment method on the original purchase. Digital River will then refund any additional amounts to the Gift Card, up to the amount paid with a Gift Card on the original purchase.

{% hint style="info" %}
**Note**: Digital River will never refund more to any payment instrument than what was originally paid using that payment instrument on the original purchase.
{% endhint %}

![](<.gitbook/assets/Refunding orders with Gift Card (1).png>)

### Tax identification numbers

The Digital River Extension allows shoppers to enter their **Tax Identification Number** during order placement, have the ID validated, and, if appropriate, the order totals will be updated accordingly.

The shopper must:

1. Check the **This is a Business Purchase** box on the **Shipping Address** screen, when purchasing physical goods, or on the **Payment Information** screen when purchasing digital or virtual goods.\
   &#x20;![](<.gitbook/assets/Tax ID number 1 (7).png>)\
   &#x20;![](<.gitbook/assets/Tax ID number 2 (4).png>)&#x20;
2. Enter the **Tax ID** and click **Apply**. &#x20;

#### **Order summary before application of the Tax ID**&#x20;

![](<.gitbook/assets/Tax ID number 4 (2).png>)

#### **Order summary after application of the Tax ID**&#x20;

![](<.gitbook/assets/Tax ID number 5 (2).png>)

### VAT invoices and credit memos

Shoppers are able to find and download a PDF of their official VAT Invoices and Credit Memos in their **My Account** screen, for authenticated shoppers, or their **Order Lookup** screen, for guest shoppers. As Digital River is the MOR/SOR, the official invoices must come from Digital River. To that end, the links on the **Invoice** and **Credit Memo** screens replace the standard Magento **Invoice** and **Credit Memo** display. &#x20;

{% hint style="info" %}
**Note**: It can take up to an hour after orders have been completed or credit memos given for the links to appear on these pages.
{% endhint %}

![](<.gitbook/assets/VAT invoice 1 (5).png>)

![](<.gitbook/assets/VAT invoice 2 (2).png>)

![](<.gitbook/assets/VAT invoice 4 (1).png>)



