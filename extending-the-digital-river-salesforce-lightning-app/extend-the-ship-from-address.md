---
description: Learn how to extend the Ship From Address.
---

# Extend the Ship From Address

The current version of the Salesforce Lightning app provides an extension point for setting the **Ship From Address** (Warehouse location) based on the client’s business requirements. After implementation, this extension point will override the **Ship From Address** attributes specified in the Digital River App settings.

The Digital River app provides a [configuration](../operation-and-maintenance/step-3-configure-the-salesforce-lightning-app.md) called the **Ship From Address - Provider Name**. If this configuration is empty (that is, the Default setting), the application uses the Ship From Address static configuration defined in other fields of the Digital River app.

An administrator has the ability to implement an Apex interface that the Digital River application delivers as part of the package, `DRB2B_CheckoutFromAddressProvider`.

The Apex class that implements this interface can be specified as a provider of Ship from Address information for the checkout flow.

An example of such a class is `CustomCheckoutShipFromAddressProvider`.

#### Sample code for this class

```
global class CustomCheckoutShipFromAddressProvider implements 
digitalriverv3.DRB2B_CheckoutFromAddressProvider {
    global digitalriverv3.DRB2B_Address 
    getAddress(digitalriverv3.DRB2B_CheckoutContext context) {
        digitalriverv3.DRB2B_Address address = new 
        digitalriverv3.DRB2B_Address ();
 
  Id cartId = context.cartId;

        // Add business logic
        address.country = 'US';
        address.state = 'NY';
        address.postalCode = '31232';
        address.city = 'New York';
        address. line1 = '123 Main St.';
 
        return address;
    }
}
```

The `getAddress` (context) method takes in a checkout context as input as shown above.

Currently, the `CartId` is passed in the Checkout context. The `Cartid` is obtained by using `context.cartId`.

The name of the class can be specified in the `Ship from Address - Provider Name` field of the Digital River App configuration.  &#x20;

![](<../.gitbook/assets/Ship from Address provider name field.png>)



