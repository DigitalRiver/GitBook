---
description: Learn how to extend the Ship from address.
---

# Extend the Ship from address

The current version of the App provides an extension point for setting the **Ship From Address** (Warehouse location) based on the client’s business requirement.

**Extension for Ship from Address**: The interface digitalriverv2.DRB2B\_ShipFromAddressInterfaceV2 needs to be implemented to extend the App's ShipFromAddress functionality.

**global Map \<String, Object> getShipFromAddressInfo(Map\<String, Object> inputData)**. This method is called when posting the user and cart information to Digital River to get the tax value. Out of the box, the App uses the **Ship From Address** values configured in the **General Config** tab of the **Salesforce B2B Commerce App**.

## **Inputs (Required)**:&#x20;

**Map \<String, Object>** that must include the following required key(s): **cart:** Specifies the CC Cart (ccrz\_\_E\_Cart\_\_c) for which Ship From Address (warehouse location) needs to be evaluated.

## **Output**:

**Map\<String, Object>**: This should contain the following information `addressLine1`, `addressLine2`, `city`, `stateCode`, `countryCode`, and `postalCode`of warehouse location.

Implementing an extension is a two-step process. To override the default App implementation:

1. Extend the Salesforce B2B Commerce App extension point. That is, implement the interface `digitalriverv2.DRB2B_ShipFromAddressInterfaceV2` and provide the implementation for the method `getShipFromAddressInfo(Map<String, Object> inputData)`.  [Example 1](broken-reference) shows the method that should be used for writing the client-specific custom code for getting Ship From Address information. [Example 2](broken-reference) shows an example of how the extension point can be used to populate the `shipFrom` address. Use this extension point to implement code to meet your business requirements.
2. Configure the App to use this extension class as follows:
   * Go to the **digitalriverv2\_\_DR\_Connector\_Extension\_Configuration\_\_mdt** metadata type.
   * Click **Manage DR Connector Extension Configurations**.
   * Open the **Ship From Address** metadata record. \
     ![](<../.gitbook/assets/Install DR B2B API Connector93.png>)
   * Update the **Extension Class** field with the previously created Custom Class name.\
     ![](broken-reference)

## Example 1

```javascript
global class drb2b_myproj_shipFromAddress implements digitalriverv2.DRB2B_ShipFromAddressInterfaceV2 {
    global Map<String, Object> getShipFromAddressInfo(Map<String, Object> inputData) {
        //implementation specific code here
    }
}
```

## Example 2

```javascript
global class drb2b_myproj_shipFromAddress implements digitalriverv2.DRB2B_ShipFromAddressInterfaceV2 {
{
    global Map<String, Object> getShipFromAddressInfo(Map<String, Object> inputData) {
        // Get Cart from Input Data
        ccrz__E_Cart__c ccCart = (ccrz__E_Cart__c) inputData.get('cart');
        String cartId = ccCart.Id;

        // Populate Ship From Address
        Map<String, Object> outputData = new Map<String, Object>();
        outputData.put('addressLine1', '123 Main St');
        outputData.put('addressLine2', '');
        outputData.put('city', 'Plainsboro');
        outputData.put('stateCode', 'NJ');
        outputData.put('countryCode', 'US');
        outputData.put('postalCode', '08536');
        return outputData;
    }
}
```
