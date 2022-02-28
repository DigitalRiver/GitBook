---
description: Learn how to override the default App implementation.
---

# Step 16: Override the default App implementation

Each Salesforce B2B Commerce implementation comes with its own business requirements and unique challenges. While OOTB (Out of the Box) App for Salesforce B2B Commerce can solve some of these challenges with specific configurations, sometimes the business requirements cannot be fulfilled in a configurable manner. That is, the solution requires code. To address these challenges, we provide extension points within the App. These extension points are called by the core app code and allow you to meet specific business requirements for each implementation.

The current version of the App provides an extension point for setting the **Ship From Address** (Warehouse location) based on the client’s business requirement.

**Extension for Ship from Address**: digitalriverv2.DRB2B\_ShipFromAddressInterface. The digitalriverv2.DRB2B\_ShipFromAddressInterface extension is used to extend the App's ShipFromAddress functionality.

**global Map getShipFromAddressMap()**. This method is called when posting the user and cart information to Digital River to get the tax value. Out of the box, the App uses the **Ship From Address** values configured in the **General Config** tab of the **Salesforce B2B Commerce App**.

## **Inputs**:&#x20;

None

## **Output**:

**Map\<String, String>**: This contains `addressLine1`, `addressLine2`, `city`, `stateCode`, countryCode, and `postalCode`.

Implementing an extension is a two-step process. To override the default App implementation:

1. Extend the Salesforce B2B Commerce App extension point. That is, implement the interface `digitalriverv2.DRB2B_ShipFromAddressInterface` and provide the implementation for the method `getShipFromAddressMap()`.  [Example 1](step-16-override-the-default-app-implementation.md#example-1) shows the constructor that should be used to create this extension. [Example 2](step-16-override-the-default-app-implementation.md#example-2) shows an example of how the extension point can be used to populate the shipFrom address. Utilize this extension point to implement code to meet your business requirements.
2. Configure the App to use this extension class as follows:
   * Go to the **digitalriverv2\_\_DR\_Connector\_Extension\_Configuration\_\_mdt** metadata type.
   * Click **Manage DR Connector Extension Configurations**.
   * Open the **Ship From Address** metadata record. \
     ![](<../.gitbook/assets/Install DR B2B API Connector93.png>)
   * Update the **Extension Class** field with the previously created Custom Class name.\
     ![](<../.gitbook/assets/Install DR B2B API Connector94.png>)

## Example 1

```
global class drb2b_myproj_shipFromAddress implements digitalriverv2.DRB2B_ShipFromAddressInterface
{
     global Map<String, String> getShipFromAddressMap() {
          //implementation specific code here
     }
}
```

## Example 2

```
global with sharing class DRB2B_ExtensionShipFromAddress implements digitalriverv2.DRB2B_ShipFromAddressInterface {
        global Map<String, String> getShipFromAddressMap() {
        Map<String, String> shipFromAddressMap = new Map<String, String>();
        // Populate Shipping Address
        shipFromAddressMap.put('addressLine1', '123 Main St');
        shipFromAddressMap.put('addressLine2', '');
        shipFromAddressMap.put('city', 'Plainsboro');
        shipFromAddressMap.put('stateCode', 'NJ');
        shipFromAddressMap.put('countryCode', 'US');
        shipFromAddressMap.put('postalCode', '08536');
        return shipFromAddressMap;
    }
}
```
