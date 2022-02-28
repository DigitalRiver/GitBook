---
description: Learn how to create page labels.
---

# Step 9: Create page labels

You can use CC Page labels to add useful Salesforce B2B Commerce App information such as help text or error messages.

{% hint style="info" %}
Download the **DR-PageLabel-DataImport-File-CSV - Sheet.csv** file for this task. It contains the page label information you need to import.
{% endhint %}

{% file src="../.gitbook/assets/DR-PageLabel-DataImport-File-CSV - Sheet.csv" %}
DR-PageLabel-DataImport-File-CSV - Sheet.csv
{% endfile %}

## Step 9a: Install the Data Loader on your local system <a href="#step-9a-install-the-data-loader-on-your-local-system" id="step-9a-install-the-data-loader-on-your-local-system"></a>

You will use the Data Loader to upload the page labels. To install the Data Loader:

1. Click **Setup** ![](../.gitbook/assets/Setup.png) and select **Setup** from the dropdown list.
2. Type `dataloader` in the **Quick Find** field and press **Enter**. \
   ![](../.gitbook/assets/search-for-data-loader.png)
3. Click **Data Loader**. The Data Loader page appears. \
   ![](../.gitbook/assets/data-loader-page.png)
4. Click the appropriate link to download and install the Data Loader for your system.
5. Click the appropriate Installation Instructions link and follow the instructions to install the Data Loader.

## Step 9b: Upload the CC Page Labels for the Salesforce B2B Commerce App <a href="#step-9b-upload-the-cc-page-labels-for-the-digital-river-app" id="step-9b-upload-the-cc-page-labels-for-the-digital-river-app"></a>

{% hint style="warning" %}
Install the [Data Loader](step-9-create-page-labels.md#step-8a-install-the-data-loader-on-your-local-system) before you upload the page labels.
{% endhint %}

1. Go to the location where you installed the Data Loader on your local system and double-click **dataloader.bat**. \
   ![](../.gitbook/assets/dataloader-bat.png)
2. &#x20;From the Data Loader app, click **Upsert**. \
   ![](../.gitbook/assets/Data-Loader-page.png)
3. Select **Password Authentication**.
4. Enter your user credentials for your Salesforce Org, where you need to upload the Page labels and click **Log in**. \
   ![](../.gitbook/assets/Salesforce-log-in.png)
5. Choose the **CC Page Label (ccrz\_\_E\_PageLabel\_\_c)** object from the list.\
   &#x20;![](../.gitbook/assets/select-data-objects.png)
6. Click **Browse**, locate the **DR-PageLabel-DataImport-File-CSV - Sheet.csv** on your system, and then click **Next**.
7. Select **ccrz\_\_PageLabelId\_\_c** as the external ID field from the dropdown list and click **Next**.\
   &#x20;![](../.gitbook/assets/choose-your-field-to-use-for-matching.png)
8. Click **Create Or Edit a Map** to map your fields (CSV columns) to the Salesforce object and click **Next**.\
   &#x20;![](../.gitbook/assets/Mapping.png)
9. In the Mapping Dialog, map the fields as shown in the following image and click **OK**:\
   ![](../.gitbook/assets/Mapping-Dialog.png)
10. Click **Browse**, locate the directory where you want to save success and error files, and then click **Finish**. \
    ![](../.gitbook/assets/Finish.png) \
    The Data Loader app upserts your records. \
    ![](../.gitbook/assets/Operation-Finished.png)
11. Click **View Errors** and check for failures. If there are any failures, correct the problem and try again.
12. Click **OK**.
13. Click **App Launcher** ![](../.gitbook/assets/App-Launcher.png) .
14. Type `Digital River App` in the **Search apps and items** field. \
    ![](../.gitbook/assets/Search-apps-and-items.png)​
15. Click the **CC Admin** tab, and then click **Indexing**. \
    ![](../.gitbook/assets/CC-Admin-Indexing.png)
16. Click **Refresh Page Label Cache**. \
    ![](../.gitbook/assets/Page-Lable-Cache.png) \
    You've completed the upsert process for the Digital River B2B CC Page Labels from the **DR-PageLabel-DataImport-File-CSV - Sheet.csv** file.
