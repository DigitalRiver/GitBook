---
description: Learn how to configure DCM logs.
---

# Step 4: Configure DCM logs

All Salesforce Lightning app application logs are captured in a Custom object called DCM Application Logs.

{% hint style="info" %}
The default Logging Level is always set to ERROR. Set the default Logging Level to WARN in production. Valid values for the Logging Level include DEBUG, INFO, WARN, and ERROR. &#x20;
{% endhint %}

The Logging framework comes with options to configure the Logging Level and Retention Days at the Org Level, Profile Level, and User Level.

1. In the **Setup** menu, open **Custom Settings**, then click the **Digital River - Logger Settings** object. \
   ![](<../.gitbook/assets/DCM log 1.jpg>)&#x20;
2. Click **Manage**. \
   ![](<../.gitbook/assets/DCM log 2.jpg>)&#x20;
3. Click **New** to enter the **Default Organization Level Value**.\
   &#x20;![](<../.gitbook/assets/DCM log 3.jpg>)&#x20;
4. Enter values for the **Logging level** and **Retention Days**. Valid values for the Logging Level include **DEBUG**, **INFO**, **WARN**, and **ERROR**.  \
   ![](<../.gitbook/assets/DCM log 4.jpg>)&#x20;
5. Click **Save**.
6. Click **New** in the **Default Organization Level Value** section to configure the logging level at the **Profile** or **User** level. \
   ![](<../.gitbook/assets/DCM log 5 (2).jpg>)&#x20;
7. Select **Profile** or **User** in the **Location** field.
8. Enter values for the **Logging level** and **Retention days**. Valid values for the Logging Level include **DEBUG**, **INFO**, **WARN**, and **ERROR**.  \
   ![](<../.gitbook/assets/DCM log 7.jpg>) &#x20;
9. Click **Save**.

\
