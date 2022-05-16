---
description: Learn how to configure the shipping choice extension point
---

# Shipping choice extension point

The Digital River app provides an extension point for setting additional details for the [shipping choice](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/shipping-choice) element such as `serviceLevel` and `description` based on the client’s business requirements. The checkout request sends this information, if provided, to Digital River.

The Digital River app provides a [configuration ](../integrate-the-salesforce-lightning-app/step-2-configure-the-digital-river-app.md)called Shipping Choice Info - Provider Name.

If this configuration is empty (default setting), the application will not send `serviceLevel` and `description` information in the shipping choice element of the checkout request.

You can implement an Apex interface that Digital River Application delivers as part of the `DRB2B_ShippingChoiceProvider` package.

You can specify the Apex class that implements this interface as a provider of Shipping Choice information for the checkout flow.

An example of such a class is `customShippingChoiceProvider`.

The following example provides sample code for this class:

```json
global class customShippingChoiceProvider implements digitalriverv3.DRB2B_ShippingChoiceProvider {
    global digitalriverv3.DRB2B_ShippingChoiceInfo getShippingChoiceInfo(digitalriverv3.DRB2B_CheckoutContext context) {
        Id cartId = context.cartId;
        Id deliveryMethodId = [SELECT DeliveryMethodId FROM CartDeliveryGroup where CartId =:cartId WITH SECURITY_ENFORCED][0].DeliveryMethodId;
        OrderDeliveryMethod orderDeliveryRec = [SELECT Description,Carrier FROM OrderDeliveryMethod where Id =: deliveryMethodId];
        digitalriverv3.DRB2B_ShippingChoiceInfo shippingChoiceInfo = new digitalriverv3.DRB2B_ShippingChoiceInfo();
        shippingChoiceInfo.serviceLevel = orderDeliveryRec.Carrier;
        shippingChoiceInfo.description = orderDeliveryRec.Description;       
        return shippingChoiceInfo; 
```

{% hint style="info" %}
If the value for either `serviceLevel` or `description` is missing for a specific Delivery Method, the checkout request will omit the field.
{% endhint %}
