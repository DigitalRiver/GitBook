---
description: Set up the Salesforce B2C LINK Cartridge and Business Manager.
---

# Configure the Salesforce B2C LINK Cartridge

## Custom site preferences

After successfully importing the metadata, select **BM Merchant Tools**, select **Site Preferences**, and then select **Custom Preferences** to see Custom Site Preferences Groups.

![](.gitbook/assets/CustomSitePref.png)

Click **Digital River** to see the cartridge setup fields.

​![](.gitbook/assets/CARTRI\~2.PNG)

| #  | Field Title                            | Description                                                                                                                                                                                                                                                        |
| -- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | Enable Digital River                   | Turns on/off Digital River integration                                                                                                                                                                                                                             |
| 2  | \*API Key                              | Digital River publishable API key                                                                                                                                                                                                                                  |
| 3  | \*Digital River public key             | Your public API key                                                                                                                                                                                                                                                |
| 4  | \*ManufacturerId                       | Manufacturer ID number                                                                                                                                                                                                                                             |
| 5  | Digital River ship from country        | The ship-from country for physical products                                                                                                                                                                                                                        |
| 6  | Digital River ship from state          | The ship-from state for physical products                                                                                                                                                                                                                          |
| 7  | Digital River ship from city           | The ship-from city for physical products                                                                                                                                                                                                                           |
| 8  | Digital River ship from address line 1 | The ship-from address line 1 for physical products                                                                                                                                                                                                                 |
| 9  | Digital River ship from address line 2 | The ship-from address line 2 for physical products                                                                                                                                                                                                                 |
| 10 | Digital River ship from postal code    | The ship-from postal code for physical products                                                                                                                                                                                                                    |
| 11 | SKUs update requested                  | The switch for the possibility of performing the job `OptionalDigitalRiverSKUsUpdate`. If you configure the job to run according to a schedule, then the Yes value will allow the job to perform its actions. See the [user guide](user-guide.md) for information. |

\*Digital River provides the values for these fields.

### Business Manager roles and permissions <a href="#business-manager-roles-and-permissions" id="business-manager-roles-and-permissions"></a>

To enable the Digital River Business Manager extensions, add the **Write** permission to the targeted access role. This is optional to enable the **Digital River Service Checker** and **Request SKUs** to update modules.

In Business Manager, select **Administration**, and then select **Roles and Permissions**. To add the Digital River modules to a role, click the role you want to modify (or create a new one). Then click one or more checkboxes to select the **Business Manager** modules for that role.

![](.gitbook/assets/BusMgrContext.png)

In the next menu, add the **Write** permission to the Digital River group as indicated below.

![](.gitbook/assets/BusMgrModule.png)

See [Business Manager](configure-the-salesforce-b2c-link-cartridge.md#business-manager) for more information about Digital River modules.

Lastly, the order status update job must be able to access the order to update the status of the order properly. To enable this job to function properly, you must change the site settings.

1. Select **Merchant Tools**, select **Site Preferences**, and click **Order**.
2. Set **Limit Storefront Order Access** to **No**.
3. Set **Storefront Order Filter by Customer Session** to **No**. \
   ![](.gitbook/assets/ORDERA\~1.PNG)
