---
description: Learn how to create page labels.
---

# Step 2: Create page labels



You can use CC Page labels to add useful Salesforce B2B Commerce App information such as help text or error messages.



{% hint style="info" %}
Download the **DR\_OrderAPI\_PageLabel-v2\_1\_1.csv** file for this task. It contains the page label information you need to import.&#x20;
{% endhint %}

{% file src="../.gitbook/assets/DR_OrderAPI_PageLabel_v2.1.1.csv" %}

## Step 2a: Install the Data Loader on your local system <a href="#step-8a-install-the-data-loader-on-your-local-system" id="step-8a-install-the-data-loader-on-your-local-system"></a>

You will use the Data Loader to upload the page labels. To install the Data Loader:

1. Click **Setup** ![](<../.gitbook/assets/setupicon (8) (1).png>) and select **Setup** from the dropdown list.
2. Type `dataloader` in the **Quick Find** field and press **Enter**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector54.png>)
3. Click **Data Loader**. The Data Loader page appears.&#x20;
4. Click the appropriate link to download and install the Data Loader for your system.
5. Click the appropriate Installation Instructions link and follow the instructions to install the Data Loader.

![](<../.gitbook/assets/Install DR B2B API Connector55.png>)

## Step 2b: Upload the CC page labels for the Salesforce B2B Commerce App <a href="#step-8b-upload-the-cc-page-labels-for-the-digital-river-app" id="step-8b-upload-the-cc-page-labels-for-the-digital-river-app"></a>

{% hint style="warning" %}
Install the [Data Loader](step-2-create-page-labels.md#step-8a-install-the-data-loader-on-your-local-system) before you upload the page labels.
{% endhint %}

1. Go to the location where you installed the Data Loader on your local system and double-click **dataloader.bat**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector56.png>)
2. &#x20;From the Data Loader app, click **Upsert**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector57.png>)
3. Select **Password Authentication**.
4. Enter your user credentials for your Salesforce Org, where you need to upload the page labels and click **Log in**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector58.png>)
5. Choose the **CC Page Label (ccrz\_\_E\_PageLabel\_\_c)** object from the list. ![](<../.gitbook/assets/Install DR B2B API Connector59.png>)
6. Click **Browse**, locate the **DR\_OrderAPI\_PageLabel.csv** file on your system, and then click **Next**.
7. Select **ccrz\_\_PageLabelId\_\_c** as the external ID field from the dropdown list and click **Next**. \
   ![](<../.gitbook/assets/Install DR B2B API Connector60.png>)
8. Click **Create Or Edit a Map** to map your fields (CSV columns) to the Salesforce object and click **Next**.\
   ![](../.gitbook/assets/install-dr-b2b-api-connector61.png)
9. Use the option to **Auto match fields with column** as shown in the following image and click OK:: \
   ![](../.gitbook/assets/Step2PageLabels9.png)
10. Click **Browse**, locate the directory where you want to save success and error files, and then click **Finish**. \
    ![](<../.gitbook/assets/Install DR B2B API Connector63.png>) \
    The Data Loader app upserts your records. \
    ![](<../.gitbook/assets/Install DR B2B API Connector64.png>)
11. Click **View Errors** and check for failures. If there are any failures, correct the problem and try again.
12. Click **OK**.
13. Click **App Launcher** ![](<../.gitbook/assets/applauncher (4).png>) .
14. Open the **CC Admin** tab, and then click **Indexing**. \
    ![](../.gitbook/assets/Step2#15.png)
15. Click **Refresh Page Label Cache**. \
    ![](<../.gitbook/assets/Install DR B2B API Connector67.png>) \
    You've completed the upsert process for the Digital River B2B CC page labels from the page labels CSV file.&#x20;
