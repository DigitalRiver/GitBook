---
description: Learn how to provide permission sets.
---

# Step 13: Manage permission sets

## Provide permission sets

To provide permissions for standard objects and fields, run the following script once from the developer console. Note that this class is outside of the package.

{% code title="Permission script" %}
```
PermissionSet pr = new PermissionSet(Label='DRB2B Additional Permission set',Name='DRB2B_Additional_Permission_set');
        insert pr;
        System.debug('pr >'+pr);
        List<ObjectPermissions>  objectPermissionList = new List<ObjectPermissions>();
 
        ObjectPermissions objPermission = new ObjectPermissions();
        objPermission.PermissionsCreate=true;
        objPermission.PermissionsRead=true;
        objPermission.PermissionsEdit=true;
        objPermission.PermissionsDelete=true;
        objPermission.SobjectType='ORDER';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        objPermission = new ObjectPermissions();
        objPermission.PermissionsCreate=true;
        objPermission.PermissionsRead=true;
        objPermission.PermissionsEdit=true;
        objPermission.PermissionsDelete=true;
        objPermission.SobjectType='Ordersummary';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        objPermission = new ObjectPermissions();
        objPermission.PermissionsCreate=true;
        objPermission.PermissionsRead=true;
        objPermission.PermissionsEdit=true;
        objPermission.PermissionsDelete=true;
        objPermission.SobjectType='WebStore';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        objPermission = new ObjectPermissions();
        objPermission.PermissionsCreate=true;
        objPermission.PermissionsRead=true;
        objPermission.PermissionsEdit=true;
        objPermission.PermissionsDelete=true;
        objPermission.SobjectType='WebCart';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        objPermission = new ObjectPermissions();
        objPermission.PermissionsCreate=true;
        objPermission.PermissionsRead=true;
        objPermission.PermissionsEdit=true;
        objPermission.PermissionsDelete=true;
        objPermission.SobjectType='Product2';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        objPermission = new ObjectPermissions();
        objPermission.PermissionsRead=true;
        objPermission.SobjectType='Account';
        objPermission.ParentId = pr.Id;
        objectPermissionList.add(objPermission);
 
        insert objectPermissionList;
        List<FieldPermissions> fieldPermissionList = new List<FieldPermissions>();
        //OrderSummary Object fields
        FieldPermissions fp= new FieldPermissions();
        //OrderItem Object fields
        fp.Field='OrderItem.TotalTaxAmount';//the name of new field
        fp.ParentId = pr.Id;
        fp.PermissionsRead=true;
        fp.SobjectType='OrderItem';
        fieldPermissionList.add(fp);
 
        fp= new FieldPermissions();
        fp.Field='Product2.Productcode';//the name of new field
        fp.ParentId = pr.Id;
        fp.PermissionsEdit=true;//
        fp.PermissionsRead=true;
        fp.SobjectType='Product2';
        fieldPermissionList.add(fp);
 
        fp= new FieldPermissions();
        fp.Field='Product2.StockKeepingUnit';//the name of new field
        fp.ParentId = pr.Id;
        fp.PermissionsEdit=true;//
        fp.PermissionsRead=true;
        fp.SobjectType='Product2';
        fieldPermissionList.add(fp);
 
        fp= new FieldPermissions();
        fp.Field='Product2.DisplayUrl';//the name of new field
        fp.ParentId = pr.Id;
        fp.PermissionsEdit=true;//
        fp.PermissionsRead=true;
        fp.SobjectType='Product2';
        fieldPermissionList.add(fp);
 
        fp= new FieldPermissions();
        fp.Field='Product2.QuantityUnitOfMeasure';//the name of new field
        fp.ParentId = pr.Id;
        fp.PermissionsEdit=true;//
        fp.PermissionsRead=true;
        fp.SobjectType='Product2';
        fieldPermissionList.add(fp);
 
        Insert fieldPermissionList;
```
{% endcode %}

## Sharing settings&#x20;

Ensure that the Sharing Settings for the Order object are set to **Public Read/Write**. If the Order object is set to **Controlled by Parent**, the Sharing Settings for Account and Contract should be **Public Read/Write**.

![](../.gitbook/assets/Sharingsettings.PNG)

## Digital River permission sets

| Permission set                       | Description                                                                                                                          |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| Digital River Connector - Admin      | Assign this permission set to Admin users to access the **Digital River App Configuration** page and to update configurations in it. |
| DigitalRiver Connector - Shopper     | Assign this permission set to all Storefront users.                                                                                  |
| DigitalRiver Connector - Integration | Assign this permission set to the Integration users.                                                                                 |
| DigitalRiver Connector - Refunds     | Assign this permission set to customer service representatives (CSRs) who initiate the refunds.                                      |

## Assign users to a permission set

To assign users to a permission set:

1. Type **Permission Sets** in the **Search** field and press **Enter**.\
   &#x20;![](<../.gitbook/assets/Permission set 1.png>)&#x20;
2. Click **Permission Sets**. The **Permission Sets** page appears.
3.  In the **Permission Set Label** column, click the permission set you want to add users to.\
    &#x20;![](<../.gitbook/assets/Permission set 2.png>)&#x20;

    This example shows how to assign a **Digital River Connector – Admin** permission set to users. ![](<../.gitbook/assets/Permission set 1 (1).png>)&#x20;
4. On the **Permission Set** page, click **Manage Assignments**.\
   &#x20;![](<../.gitbook/assets/Permission set 4.png>)&#x20;
5. Click **Add Assignments**.\
   &#x20;![](<../.gitbook/assets/Permission set 5.png>)&#x20;
6. Select one or more users who you want to assign to this permission set and click **Assign**. The assigned users now appear in the modified permission set.\
   &#x20;![](<../.gitbook/assets/Permission set 6.png>)&#x20;

See the [Digital River permission sets table](step-13-manage-permission-sets.md) to repeat the above-mentioned steps for assigning relevant permission sets.
