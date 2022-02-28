---
description: Learn how to configure CC Admin settings.
---

# Step 9: Configure CC Admin settings

## Step 9a: Create a service override for the Tax Calculation API class <a href="#step-9a-create-a-service-override-for-the-tax-calculation-api-class" id="step-9a-create-a-service-override-for-the-tax-calculation-api-class"></a>

Salesforce B2B Commerce (CloudCraze) does not calculate taxes out-of-the-box (OOTB). Instead, it exposes a Tax Calculation webhook which you must override. This step will implement the new business-specific tax calculations by making a call to Digital River for tax calculations to override the Tax Calculation webhook.

To create service override for the Tax Calculation API class:

1. Go to **CC Admin**.
2. Select **Storefront** from the **Global Settings** dropdown list.
3. Click **Tax** under **Integrations**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector68.jpg>)
4. Set the Tax Calculation API class to **digitalriverv2.DRB2B\_CartTaxCalculation** as shown in the screenshot above.
5. Click **Save**.

## Step 9b: Create configuration module for payment type <a href="#step-9b-create-configuration-module-for-payment-type" id="step-9b-create-configuration-module-for-payment-type"></a>

Create a Configuration Module for Digital River payment type. You perform this step at the Global Settings level. The changes you make here apply to all your storefronts.

1. Select the **CC Admin** tab.
2. Select **Configuration Modules**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector69.jpg>)
3. Create a module for Digital River payment.
   * Click **New** in the **Configuration Module** pane. The Configuration Module dialog appears.
   * Type `Payment DR` in the **Name** field and `pmt_dr` in the **API Name** field.&#x20;

![](<../.gitbook/assets/Install DR B2B API Connector70.jpg>)

## Step 9c: Create configuration metadata for Payment DR Module

Configure the following custom Salesforce B2B Commerce App pages in CC Admin. They will appear in the following storefront locations: Edit Page, New Page, Pay Page, and Proc. Note that you perform this step at the Global Settings-level. The changes you make here apply to all your storefronts.

The Payment DR module should pull in all payment types configured by Digital River.

To create configuration settings for the Payment DR configuration modules:

1. Under **Configuration Modules**, click the **Payment DR** module.
2. Click **New** to create the Edit Page configuration metadata for the configuration module.\
   ![](<../.gitbook/assets/Install DR B2B API Connector71.jpg>)
3. Use the information associated with the [module](step-9-configure-cc-admin-settings.md#modules) to complete the Edit Page configuration metadata.\
   &#x20;![](<../.gitbook/assets/Install DR B2B API Connector72.png>) \
   **Note**: Don’t select the **Externally Safe** check box.
4. Repeat steps 2 and 3 to create configuration metadata for New Page, Pay Page, and Proc. After adding the configuration metadata to the Payment Module DR, the Configuration Module should look like this:&#x20;

![](<../.gitbook/assets/Install DR B2B API Connector72.jpg>)

### Modules <a href="#modules" id="modules"></a>

The following table lists the required settings for each field.

| Module         | Name      | API Name | Description                                                                                   |
| -------------- | --------- | -------- | --------------------------------------------------------------------------------------------- |
| **Payment DR** | Edit Page | edit     | Edit page for Payment DR                                                                      |
| **Payment DR** | New Page  | new      | VisualForce page leveraged for saving new Drop-in payment information via the My Account page |
| **Payment DR** | Pay Page  | pay      | VisualForce page for rendering the Payment DR on the Checkout page                            |
| **Payment DR** | Proc      | proc     | Payment processor for backend processing                                                      |

## Step 9d: Create configuration settings for a storefront <a href="#step-9d-create-configuration-settings-for-a-storefront" id="step-9d-create-configuration-settings-for-a-storefront"></a>

{% hint style="info" %}
Custom Salesforce B2B Commerce App pages must be configured in CC Admin for them to show up in your storefront. Note that you perform this step at the storefront level. The changes you make here apply to a specific storefront. If you have more than one storefront, you should repeat this step for each storefront.
{% endhint %}

To create or update a store's configuration settings:

1. From **CC Admin**, click **Global Settings** in the upper-right corner and select your storefront (for example, **DefaultStore**). \
   ![](<../.gitbook/assets/Install DR B2B API Connector73.png>) \
   **Note**: After selecting the storefront, the select box will still display Global Settings. However, the left navigation pane will display _\<storefront name>_SETTINGS and the options associated with the store.
2. Click **Configuration Settings** under **<**_**storefront name**_**> SETTINGS.** ![](<../.gitbook/assets/Install DR B2B API Connector74.png>)
3. Select the module name (for example, Body Includes Begin from [Modules](step-9-configure-cc-admin-settings.md#modules-1)) from the **Module** dropdown list. \
   ![](<../.gitbook/assets/Install DR B2B API Connector75.png>)
4. To create a new page setting for the module, click **New**. The New Page Setting dialog appears.\
   &#x20;![](<../.gitbook/assets/Install DR B2B API Connector76.png>)
5. Complete the fields using the information from the [Modules](step-9-configure-cc-admin-settings.md#modules-1) table.
   * Select the module name from the **Module** dropdown list.
   * Select the configuration value from the **Configuration** dropdown list.
   * Type the page value in the **Page** field and select the corresponding value. Once you select it, the field shows a corresponding internal value. For example, if you type `Order Confirmation` and select **Order Confirmation** from the dropdown list, the field shows **OrdCnfm**.
   * Type the value in the **Value** field.
   * Click **Create**. The new module appears in the Configure Settings list and displays **Delete** in the **ACTION** column, and the name of the storefront appears in the **STOREFRONT** column.
6. Repeat steps 3 through 5 for each additional row in the [Modules](step-9-configure-cc-admin-settings.md#modules-1) table.
7. Repeat steps 1 through 6 for each additional storefront.

### Modules <a href="#modules-1" id="modules-1"></a>

The following table lists the DR Configuration Settings that need to be configured for each storefront:

| Module              | Configuration        | Page               | Value                                                                   |
| ------------------- | -------------------- | ------------------ | ----------------------------------------------------------------------- |
| Body Includes Begin | Enabled              | Order View         | TRUE                                                                    |
| Body Includes Begin | Enabled              | Order Confirmation | TRUE                                                                    |
| Body Includes Begin | Enabled              | Check Out          | TRUE                                                                    |
| Body Includes Begin | Page Include Name    | Order VIew         | digitalriverv2\_\_DRB2B\_OrderConfirmation                              |
| Body Includes Begin | Page Include Name    | Order Confirmation | digitalriverv2\_\_DRB2B\_OrderConfirmation                              |
| Body Includes Begin | Page Include Name    | Check Out          | digitalriverv2\_\_DRB2B\_OrderReview                                    |
| Body Includes End   | Enabled              | My Account         | TRUE                                                                    |
| Body Includes End   | Enabled              | Check Out          | TRUE                                                                    |
| Body Includes End   | Page Include Name    | My Account         | digitalriverv2\_\_DRB2B\_MyAccount                                      |
| Body Includes End   | Page Include Name    | Check Out          | digitalriverv2\_\_DRB2B\_PaymentProcessor\_Checkout                     |
| Checkout            | Payment Types        | all                | dr                                                                      |
| Checkout            | Use Default          | Check Out          | TRUE                                                                    |
| My Account          | Use Default          | My Account         | FALSE                                                                   |
| My Account          | Override Flow        | My Account         | TRUE                                                                    |
| My Wallet           | Payments             | all                | dr                                                                      |
| Order Review        | Show Total Surcharge | all                | TRUE                                                                    |
| Order Review        | Show  Surcharge      | all                | TRUE                                                                    |
| Payment             | White List           | all                | cc\_pmt\_PO\_New,cc\_pmt\_PO\_Pay, digitalriverv2\_\_DRB2B\_Payment\_DR |
| Payment DR          | New Page             | all                | digitalriverv2\_\_DRB2B\_MyWallet\_Payment\_DR                          |
| Payment DR          | Proc                 | all                | digitalriverv2.DRB2B\_CCPaymentProcessor                                |
| Payment DR          | Edit Page            | all                | digitalriverv2\_\_DRB2B\_MyWallet\_Payment\_DR                          |
| Payment DR          | Pay Page             | Check Out          | digitalriverv2\_\_DRB2B\_Payment\_DR                                    |

## Step 9e: Refresh the Configuration Cache <a href="#step-9e-refresh-the-configuration-cache" id="step-9e-refresh-the-configuration-cache"></a>

CC Admin configurations are cached. Refresh the configuration cache to ensure you can see the latest configuration changes made to the storefront.

1. Click **Global Settings** to return to the Global Settings page. \
   ![](<../.gitbook/assets/Install DR B2B API Connector77.png>)
2. Click **Configuration Cache Management** under **GLOBAL SETTINGS**. ![](<../.gitbook/assets/Install DR B2B API Connector78.png>)
3. Click **Build New**.
4. Click **Refresh List**. You may have to click the Refresh link several times before the build completes. When complete, a new configuration identifier appears under the **CONFIG ID** column.\
   ![](<../.gitbook/assets/Install DR B2B API Connector79.png>)
5. Click **Activate** under the **Status** column for the new configuration identifier and deactivate any previous configurations.
6. Locate the previous cache and click **Deactivate**.
7. To verify your changes, clear the browser cache and test the storefront pages.
8. Digital River Terms and Conditions will be displayed on the Order Review page and Digital River Payment tab and the client-specific payment methods will be displayed on the Payment page.
