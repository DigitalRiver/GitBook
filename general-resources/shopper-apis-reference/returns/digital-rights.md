---
description: >-
  Learn how digital rights are handled when a customer returns an item that has
  digital rights.
---

# Digital rights

A product’s digital rights can be either unique or identical.

* Unique Digital Rights—a shopper receives a unique serial number for each unit ordered or purchased.
* Identical Digital Rights—a shopper receives an identical serial number for every unit sold.

When a shopper returns an item that has unique digital rights, you can revoke the digital rights for the line item and quantity. When the shopper has more than one digital rights ID for the line item, the shopper must select which digital rights ID to return.

{% hint style="info" %}
**Best Practices**: Display text that tells the shopper they must select the correct digital rights key because you will deactivate it once you process the return.
{% endhint %}

When a shopper returns an item that has identical digital rights, you can revoke the digital rights when the shopper returns the entire quantity of the specified line item.

{% hint style="info" %}
**Example**: The shopper purchased a quantity of five items that have identical digital rights. You don’t revoke the digital rights until the shopper returns all five items.
{% endhint %}

If the product is digital, and the Return Type is ELOD (Electronic Letter of Destruction), you must provide the shopper the ELOD online when returning a digital product and the return request should indicate whether the shopper accepted the ELOD. You must display the ELOD legal text to the shopper. If the shopper accepts the ELOD, Digital River will suppress the ELOD email.

{% hint style="info" %}
**Note**: The value for ELOD must be set to true (ELOD = true).
{% endhint %}

For more information, see [Digital Rights](https://help.digitalriver.com/help/gc/Products/All-Products/Configuring-the-product-settings.htm#DigitalRights) in the [Global Commerce Help](https://help.digitalriver.com/help/gc.htm).
