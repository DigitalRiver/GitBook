---
description: Learn how to configure shipping integration.
---

# Step 14: Configure shipping integration

Digital River uses digital and physical products. The custom object **Digital River Tax Mapping** stores all the Tax Groups, Tax Types, Tax Codes, and Product Type information. Every Product/SKU in Salesforce should be associated with a Tax Code for the Product to be synced to Digital River.&#x20;

When the tax code (using Tax Group and Tax Type) is set on the Product, Digital River uses the specified Tax code value to classify a product as either physical or digital. This classification determines the address requirements for any orders with this SKU. Whether the product is classified as physical or digital also is used in the [determination of the selling entity](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/selling-entities#how-selling-entities-are-assigned), which affects how taxes are calculated and whether tax identifiers are applicable.

The `DR Checkout Type` custom field on the `Cart` object indicates whether a particular cart is digital or non-digital (physical or mixed).

* Digital cart contains only digital products.
* Physical cart contains only physical products.
* Mixed cart contains a combination of digital and physical products.

Digital products should not have shipping costs associated with them.

### Shipping/delivery methods/options

As part of shipping integration, the shipping and delivery methods should not be displayed for digital carts. If the shipping and delivery methods are displayed, they should contain only a **$0** option.

#### Shipping option for a digital cart

This screenshot contains only the **$0** shipping option for a digital cart.

![](<../.gitbook/assets/Digital cart shipping option.png>)

#### Shipping option for a non-digital cart

This screenshot includes more shipping options for a non-digital cart.

![](<../.gitbook/assets/Non-digital shipping option.png>)

{% hint style="info" %}
A sample **Shipping Integration** class (DRB2B\_ShippingSample.txt) has been provided for testing purposes.&#x20;
{% endhint %}

{% file src="../.gitbook/assets/DRB2B_ShippingSample.txt" %}
