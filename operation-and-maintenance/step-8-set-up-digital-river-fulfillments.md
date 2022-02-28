---
description: >-
  Learn how to create a connected app for integration between Salesforce and
  Digital River.
---

# Step 10: Set up integration between Salesforce and Digital River

## Create a connected app for integration between Salesforce and Digital River

To create a connected app for integration between Salesforce and Digital River:

1. Go to **Setup**, enter **App Manager** in the **Search** field, and then select **App Manager**.
2. Click **New Connected App**.
3. Enter the Connected App Name **Salesforce DigitalRiver Integration** and your email address.
4. Select **Enable OAuth Settings**.
5. Enter **https://** as the Callback URL.
6. In **OAuth Scopes**, add **Access and manage your data (API)**.
7. Ensure the checkbox labeled **Require Secret for Web Server Flow** is selected.&#x20;
8. Click **Save**.&#x20;

## Create a profile to assign it to an integration user

To create a profile and its assignment to an Integration User:&#x20;

1. Create a new profile **Digital River Integration User** by cloning the **Standard User** profile.
2. Set the password policy of this profile to **never expire**.
3. Create an **Integration User** and assign the user to the profile.
4. Add the user to the permission set named **DigitalRiver Connector - Integration**.



