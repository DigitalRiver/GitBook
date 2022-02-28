---
description: Learn how to import ECCN codes, tax groups, and tax types.
---

# Step 7: Import ECCN codes, tax groups, and tax types

{% hint style="warning" %}
You must load the ECCN codes, tax groups, and tax types and assign them to the Salesforce Lightning products in Salesforce before you do the [Product Sync](step-8-configure-and-synchronize-the-products.md#product-synchronization).&#x20;

Products missing any required fields (for example, DR Product Country Origin, DR TAXGROUP, DR TAXTYPE, and DR ECCN) will not be synced to Digital River. Digital River uses this information to [calculate tax](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/tax-calculations).&#x20;
{% endhint %}

To import **ECCN codes**, **Tax Groups**, and **Tax Types**:

1. Go to the **Setup** menu.
2. In the **Search** field, search for the **Data Import Wizard**.\
   &#x20;![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuSPQCR0CEVgH5dhLh%2F-McuTAUKv7fL2J8TeO-3%2FData%20import%20wizard.png?alt=media\&token=d8de4e40-7bcc-4d2c-8848-7cfc3ff31fe0)
3. Click **Launch Wizard**. \
   ![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuTJOFKJ8UwpOfmWDA%2F-McuTUUP15KumtID4Vgu%2FLaunch%20wizard.png?alt=media\&token=a073c45c-1830-4658-a351-7cf4ba8309dd)
4. Click **Digital River Tax Mappings**. \
   ![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuTJOFKJ8UwpOfmWDA%2F-McuTlg\_DWwkjDqHu0cB%2FDigital%20River%20tax%20mapping%20custom%20object.png?alt=media\&token=14bbce36-4fd1-4537-ba75-6eca27420e95)
5. Click **Add new records**.\
   &#x20;![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuTpuFVxxn3zd-7CAo%2F-McuTv7boo0I7QLGUOTQ%2FAdd%20new%20records.png?alt=media\&token=cc1a1bbf-475e-438c-83d6-30c59b1b1412)
6. Click **CSV** to upload the file. \
   ![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuTpuFVxxn3zd-7CAo%2F-McuU6PJrI1LxTh14fsl%2FCSV%20to%20upload%20the%20file.png?alt=media\&token=b6e8bfac-dbde-46ee-aaa4-33e54e46e14e)
7. Select **Choose File** and click **Next**. \
   ![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-McuUJir4CH4M1-EAlOe%2F-McuUPjE6mg0PhPP\_uTR%2FChoose%20file%20and%20click%20next.png?alt=media\&token=ce49aaac-77d0-4eae-80dc-96e7875a189c)
8. Map the **CSV** column to the **Custom Fields** column. \
   ![](<../.gitbook/assets/CSV mapping.png>)&#x20;
9. Click **Next**, then click **Start import**.&#x20;

{% hint style="info" %}
Repeat the above steps to import ECCN codes to the Digital River ECCN Lookup (Custom object).
{% endhint %}

#### **​Tax code mapping spreadsheet**

{% file src="../.gitbook/assets/Tax Code Mapping.csv" %}

#### **Approved ECCN codes spreadsheet**&#x20;

{% file src="../.gitbook/assets/Approved ECCN Codes.csv" %}
Tax code mapping spreadsheet
{% endfile %}

****[\
](https://docs.digitalriver.com/salesforce-lightning/v/1.0/operation-and-maintenance/step-6-enable-or-disable-us-tax-certificates)
