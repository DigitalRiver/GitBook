---
description: Learn how to use the bulk user management service.
---

# Bulk user management

The Bulk User Management service provides a batch interface that third-party applications and any other processes can use to manage Digital River-hosted user information in bulk form. Use this service to add, modify, or remove multiple users.

## Bulk user management service details

Third-party applications and any other processes can use a batch interface for the Bulk User Management service to manage Digital River-hosted user information in bulk form.

A few points to remember:

* BulkUserManagement performs a secure operation. Each operation requires a `loginID` and password before file processing begins.
* For optimal performance, a Bulk User Management file should not exceed 10,000 records per file.
* You must configure Bulk User Management per site.

Supported Bulk User Management tasks include:

* **Activate users**—Activate the existing users.
* **Inactivate users**—Inactivate the existing active users.
* **Reset user password**—Resets a user's password.
* **Get user information**—Get information about the Digital River-hosted shoppers.
* **Add or update users**—Add new users to or update existing users in the Digital River system. See [Add users](bulk-user-management-service.md#add-users) and [Update users](bulk-user-management-service.md#update-users) for more information.
* **Cancel subscriptions**—Deactivate subscriptions for requisitions received in a request.
* **Activate subscriptions**—Activate subscriptions for requisitions received in a request.
* **Modify the renewal date of subscriptions**—Modify the renewal date of subscriptions. The subscriptions will be set to expire on the requested renewal date as passed in by the client. The renewal reminder notification will be sent to the shopper "n" (n=3, 4, or 5) days before the expiration date of the subscription. This "n" days prior renewal reminder will be set as a product-level attribute.

{% hint style="info" %}
**Note**: You can send this call at any time. It has no restrictions other than you cannot set the renewal date earlier than the current date and make a call for a canceled or returned line item.
{% endhint %}

* **Modify renewal mechanism for a subscription (manual or auto)**—Modify the subscription renewal process. The valid values are as follows:
  * **Auto**—Converts a subscription to auto-renewal.
  * **Manual**—Converts a subscription to manual renewal.
  * **Inactive**—Converts a subscription to inactive.
* **Cancel users' orders**—Cancel the users' orders for the requisition or line item received in the request.

{% hint style="info" %}
**Note**: You must supply the `shopperKey` for all Bulk User Management tasks.
{% endhint %}

## Add users

The following table displays the minimum required fields when adding users.

| Parent Element                    | Child and Grand-Child Elements                                                                                                                                                                                                                                                                               |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `shopperKey`                      | <p></p><ul><li><code>companyId</code></li><li><code>loginId</code></li><li><code>siteId</code></li></ul>                                                                                                                                                                                                     |
| `billingOptionToBeAddedOrUpdated` | <p></p><ul><li><code>nickName</code></li><li><code>isDefault</code></li><li><code>billingOptionType</code></li></ul>                                                                                                                                                                                         |
| `billingOptionToBeAddedOrUpdated` | <p></p><ul><li><code>nickName</code></li><li><code>isDefault</code></li><li><p><code>address</code></p><ul><li><code>city</code></li><li><code>countryA2</code></li><li><code>country</code></li><li><code>countryName</code></li><li><code>line1</code></li><li><code>postalCode</code></li></ul></li></ul> |

{% hint style="info" %}
**Note**: The `addressId` is not required. The system generates the `addressId` for the new shopper.
{% endhint %}



## Update users

The following table displays the minimum required fields when updating users.

| Parent Element                         | Child and Grand-Child Elements                                                                                                                                                                                                   |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `shopperKey`                           | <p><code>userId</code> OR </p><p>(<code>externalReferenceId</code> AND <code>siteId</code>) OR </p><p>(<code>externalReferenceId</code> AND <code>companyId</code>) OR </p><p>(<code>loginId</code> AND <code>siteId</code>)</p> |
| `billingOptionToBeAddedOrUpdated`      | <p><code>key</code></p><ul><li><code>billingOptionId</code></li></ul><p><code>nickName</code></p><p><code>isDefault</code></p><p><code>billingOptionType</code></p>                                                              |
| `billingOptionToBeDeleted`             | `billingOptionID`                                                                                                                                                                                                                |
| `addressBookEntiresToBeAddedOrUpdated` | <p><code>key</code></p><ul><li><code>addressBookEntryID</code></li></ul><p><code>nickName</code><br><code>isDefaullt</code><br><code>address</code></p>                                                                          |
| `addressBookEntriesToBeDeleted`        | `addressBookEntryID`                                                                                                                                                                                                             |

## Bulk user management service schemas

| Version     | Schema Components Table                                                                    | Raw Schema                                                                     | Sample XML                                                                             |
| ----------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| 7 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkUserManagement/7) | [View](https://drhadmin.digitalriver.com/integration/xsd/BulkUserManagement/7) | [View](https://drhadmin.digitalriver.com/integration/isg/example/BulkUserManagement/7) |
| 6           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkUserManagement/6) | [View](https://drhadmin.digitalriver.com/integration/xsd/BulkUserManagement/6) | [View](https://drhadmin.digitalriver.com/integration/isg/example/BulkUserManagement/6) |
| 5           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkUserManagement/5) | [View](https://drhadmin.digitalriver.com/integration/xsd/BulkUserManagement/5) | [View](https://drhadmin.digitalriver.com/integration/isg/example/BulkUserManagement/5) |
