---
description: Learn how to import ECCN codes, tax groups, and tax types.
---

# Step 6: Import ECCN codes, tax groups, and tax types

{% hint style="warning" %}
You must upload the ECCN codes, tax groups, and tax types and assign them to CC Products in Salesforce before you do the [Product Sync](step-7.-update-the-product-sync-settings.md).
{% endhint %}

Note that the ECCN codes, tax groups, and tax types provided in these files do not represent a complete list. However, it's enough to get you started.

{% hint style="info" %}
Download the `Approved-ECCN-Codes.csv` file and the `TaxGroup_TaxTypes.csv` file and save them to your computer.
{% endhint %}

{% file src="../.gitbook/assets/Approved-ECCN-Codes (2).csv" %}
Approved-ECCN-Codes.csv
{% endfile %}

{% file src="../.gitbook/assets/TaxGroup_TaxTypes (2).csv" %}
TaxGroup\_TaxTypes.csv
{% endfile %}

The UploadECCN\_Script and UploadTaxGroup\_Script contain dummy values. You can use the test values or populate them with real values for testing purposes. These files are not used in production. You can use these scripts to test a specific scenario where you need to figure out the tax group, tax type, and ECCN code for a specific product.

{% hint style="info" %}
Download the following ZIP files, extract the UploadECCN\_Script and UploadTaxGroup\_Script files, and save them to your computer.
{% endhint %}

{% file src="../.gitbook/assets/UploadECCN_Script (2).zip" %}
UploadECCN\_Script.zip
{% endfile %}

{% file src="../.gitbook/assets/UploadTaxgroup_Script (2).zip" %}
UploadTaxgroup\_Script.zip
{% endfile %}

{% hint style="warning" %}
These scripts auto-populate the ECCN and tax group for your products. This can be helpful for testing purposes rather than having to manually populate them. Be aware that the auto-population may assign tax codes that are not appropriate to a specific product (for example, a digital tax code for a physical product). Do not run in production.
{% endhint %}

## Step 6a: Import ECCN codes

To import the ECCN codes:

1. Click **Setup** ![](<../.gitbook/assets/setupicon (8) (3).png>) and select **Setup** from the dropdown list.
2. Type `data import wizard` in the **Quick Find** field and press **Enter**. ![](<../.gitbook/assets/Install DR B2B API Connector16.png>)​
3. Click **Data Import Wizard**.
4. Scroll down and click **Launch Wizard!** The Launch Wizard appears. ![](../.gitbook/assets/install-dr-b2b-api-connector23.png)
5. Click the **Custom objects** tab.
6. Scroll down and click **Digital River ECCN Lookups**.
7. Scroll up and click **Add new records**.
8. Locate the `Approved-ECCN-Codes.csv` file and drag it to **Drag CSV file here to upload** and drop it.\
   ![](<../.gitbook/assets/Install DR B2B API Connector18.png>)
9. Click **Next**. The file has been auto-mapped to existing Salesforce fields. ![](<../.gitbook/assets/Install DR B2B API Connector19.png>)
10. Click Map associated with the **"Classification Code"**, select **DR Classification Code**, and then click **Map**. \
    ![](<../.gitbook/assets/Install DR B2B API Connector20.png>)
11. Click Map associated with the **Description**, select **DR Description**, and then click **Map**.
12. Click Map associated with the **Notes**, select **DR Notes**, and then click **Map**.
13. Click **Next**. \
    ![](<../.gitbook/assets/Install DR B2B API Connector21.png>)
14. Review your import information and click **Start Import**. The import should start successfully.\
    ![](<../.gitbook/assets/Install DR B2B API Connector22.png>)
15. Click **OK**. When the import completes, you will receive an email.

## Step 6b: Import tax groups and tax types <a href="#step-5b-import-tax-groups-and-tax-types" id="step-5b-import-tax-groups-and-tax-types"></a>

To import tax groups and tax types:

1. Click **Data Import Wizard**.
2. Click **Launch Wizard!** The Launch Wizard appears. \
   ![](<../.gitbook/assets/Install DR B2B API Connector23.png>)
3. Click the **Custom objects** tab.
4. Scroll down and click **Digital River Tax code Lookups**.
5. Scroll up and click **Add new records**.
6. Locate the **TaxGroup\_TaxTypes.csv** file and drag it to **Drag CSV file here to upload** and drop it.\
   ![](<../.gitbook/assets/Install DR B2B API Connector24.png>)
7. Click **Next**. The file has been auto-mapped to existing Salesforce fields. ![](<../.gitbook/assets/Install DR B2B API Connector25.png>)
8. Click the Map associated with the **TAXGROUP**, select **DR TAXGROUP,** and then click **Map**.\
   ![](<../.gitbook/assets/Install DR B2B API Connector26.png>)
9. Click the Map associated with the **TAXTYPE**, select **DR TAXTYPE**, and then click **Map**.
10. Click the Map associated with the **SABRIXCODE**, select **DR SABRIXCODE**, and then click **Map**.
11. Click the Map associated with the **UNSPSC**, select **DR UNSPSC**, and then click **Map**.
12. Click **Next**. \
    ![](<../.gitbook/assets/Install DR B2B API Connector27.png>)
13. Review your import information and click **Start Import**. The import should start successfully.\
    ![](../.gitbook/assets/install-dr-b2b-api-connector22.png)
14. Click **OK**. When the import completes, you will receive an email.

## Step 6c: Import the ECCN and tax group scripts <a href="#step-5c-import-the-eccn-and-tax-group-scripts" id="step-5c-import-the-eccn-and-tax-group-scripts"></a>

This step is only required for development purposes. The UploadECCN\_Script and UploadTaxGroup\_Script contain dummy values. You can use the test values or populate them with real values.

{% hint style="info" %}
You need the UploadECCN\_Script and UploadTaxGroup\_Script files for this task.
{% endhint %}

To import the ECCN and tax group scripts:

1. From Salesforce B2B, click **Setup** ![](<../.gitbook/assets/setupicon (8) (7).png>) and select **Developer Console**. The Developer Console opens.\
   ![](<../.gitbook/assets/Install DR B2B API Connector29.png>)
2. &#x20;Click **Debug** and select **Open Execute Anonymous Window**. The Enter Apex Code dialog appears.\
   ![](<../.gitbook/assets/Install DR B2B API Connector30.png>)
3. Locate and open the **UploadECCN\_Script**.
4. Copy the contents of the **UploadECCN\_Script**, paste it in the **Enter Apex Code** dialog, and click **Execute**. You should see a Success status in the **Logs** tab. \
   ![](<../.gitbook/assets/Install DR B2B API Connector31.png>)
5. Locate and open the **UploadTaxGroup\_Script**.
6. Copy the contents of the **UploadTaxGroup\_Script**, paste it in the **Enter Apex Code** dialog, and click **Execute**. You should see a Success status in the **Logs** tab.

![](<../.gitbook/assets/Install DR B2B API Connector32.png>)

## Step 6**d**: Assign tax and ECCNs to products <a href="#step-5d-assign-tax-and-eccns-to-products" id="step-5d-assign-tax-and-eccns-to-products"></a>

Assign the tax group, tax type, and ECCNs to products in Salesforce B2B.

{% hint style="warning" %}
Complete this task before you [update the product sync settings](step-7.-update-the-product-sync-settings.md) with Digital River.
{% endhint %}

1. Click **App Launcher** ![](<../.gitbook/assets/applauncher (4) (2).png>) .
2. Type `CC Products` in the **Search apps and items** field.
3. Click **CC Products**.
4. Under the **Product Name** column, click the link for the product you want to update or click **New** to create a new product. \
   ![](<../.gitbook/assets/Install DR B2B API Connector34.png>)
5. Click **Edit**.
6. Scroll down to **DR ECCN** and provide a valid ECCN value in the **DR ECCN** field. ![](<../.gitbook/assets/Install DR B2B API Connector35.png>)\
   Note that the EECN Lookup component will appear at the bottom of the CC Product page:\
   ![](../.gitbook/assets/DR-ECCN-Code.png)&#x20;
7. Select the appropriate tax group from the **DR TAXGROUP** dropdown list.
8. Select the appropriate tax type from the **DR TAXTYPE** dropdown list.
9. Click **Save**.
10. Repeat steps 4 through 9 for each additional product.
