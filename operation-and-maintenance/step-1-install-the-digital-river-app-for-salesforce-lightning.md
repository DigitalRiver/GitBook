---
description: Learn how to install the Digital River app for Salesforce Lightning.
---

# Step 1: Install the Digital River app

### Install the Digital River app

{% hint style="warning" %}
Only Salesforce administrators and users with the **Download AppExchange packages** permission can install or uninstall AppExchange apps.
{% endhint %}

1. Download the Salesforce B2B Package URL version number 1.5 (1.5.0) from the [App Exchange](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3u00000PGZJCEA5).
2. Sign in to the Salesforce org where you want to install the package. After a successful login, the installation wizard appears.
3. Click **Install for Specific Profiles** and select **Full Access** for all profiles you want to use with the package.
4. Select and grant **Full Access** to the **Community Profile** that will be assigned to the **Storefront Users**.
5. After selecting profiles, click **Install/Upgrade**. Once the package is installed, the administrator receives an email. \
   ![](<../.gitbook/assets/Install DR 1 (1).jpg>)&#x20;

{% hint style="info" %}
The notification (in the above screenshot) appears when configuring the package installation settings:&#x20;

1. Before installing the package, understand that the package is not authorized for distribution.
2. The notification displays when a managed package:&#x20;
   * Has never been through security review or is under review&#x20;
   * Did not pass the security review&#x20;
   * Is not authorized by the AppExchange Partner Program for another reason
{% endhint %}

![](<../.gitbook/assets/Install DR 2.jpg>)

![](<../.gitbook/assets/Install DR 3.jpg>)

{% hint style="info" %}
If a package that has not passed the Security Review is used for installation, click the **Allow deployments of components** checkbox under **Deployment Options**.
{% endhint %}
