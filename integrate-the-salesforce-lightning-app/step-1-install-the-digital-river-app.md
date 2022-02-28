---
description: Learn how to install the Digital River app for Salesforce Lightning.
---

# Step 1: Install the Digital River app



{% hint style="warning" %}
Use the [latest package installation URL](../#system-requirements) to install or upgrade to the [latest version](../#system-requirements) of the Salesforce Lightning app:

Salesforce administrators and users with the **Download AppExchange packages** permission can **Install/Uninstall AppExchange** apps.
{% endhint %}

1. Click the installation URL and sign in to the Salesforce org where you want to install the package. After a successful login, the installation wizard appears.
2. Click **Install for Specific Profiles** and select **Full Access** for all profiles you want to use with the package.
3. Select and grant **Full Access** to the **Community Profile** that will be assigned to the **Storefront Users**.
4. After selecting profiles, click **Install/Upgrade**. Once the package is installed, the administrator receives an email. \
   &#x20;

![](<../.gitbook/assets/Install DR 1.jpg>)

{% hint style="info" %}
The notification (in the above screenshot) appears when you configure the package installation settings:&#x20;

1. Before installing the package, understand that the package is not authorized for distribution.
2. The notification displays when a managed package:&#x20;
   * Has never been through security review or is under review&#x20;
   * Did not pass the security review&#x20;
   * Is not authorized by the AppExchange Partner Program for another reason
{% endhint %}

![](<../.gitbook/assets/Install DR 2.jpg>)

![](<../.gitbook/assets/Install DR 3.jpg>)

{% hint style="info" %}
If you install a package that has not passed the Security Review, click the **Allow deployments of components** checkbox under **Deployment Options**.
{% endhint %}
