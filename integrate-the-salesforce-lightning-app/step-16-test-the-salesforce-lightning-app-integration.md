---
description: Learn how to test the Salesforce Lightning app integration.
---

# Step 16: Test the Salesforce Lightning app integration

This step assumes you have completed all installation steps thus far. Commonly missed steps include:

* Adding users to the correct permission sets
* Configuring tax codes and ECCNs for products
* Configuring custom fields on various pages
* Configuring custom components on various pages
* Configuring various flows/sub-flows

### Test the checkout flow

To test the checkout flow:

1. Log in to the storefront as a registered user.
2. Add one or more products to your cart.
3. Go to the shopping cart and click **Checkout**.
4. Enter pertinent information on the **User Information** and **Shipping** pages.&#x20;

| Page           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Review   | <p>This page is the first place where the Digital River integration is visible. It includes the following:</p><ul><li>Taxes, fees, and duties are displayed as applicable</li><li> <em>Digital River Terms and Conditions</em> </li></ul><p>For US tax-exempt purchases, the user can manage tax certificates and apply a global tax identifier, if applicable.</p><p></p><p>Tax certificates are displayed on the Buyer information page. If a new tax certificate is uploaded, a relevant API call is made to Digital River to create a customer if one does not already exist.</p> |
| Payment        | <p>On this page, the user has the option to pay using either:</p><ul><li>A stored payment method</li><li>A new payment method</li></ul><p>Available payment methods will depend on the configuration of your Digital River account. In a test environment, you may use the applicable <a href="https://docs.digitalriver.com/digital-river-api/payment-integrations-1/testing-scenarios">testing payment methods</a>.</p>                                                                                                                                                             |
| Order Complete | <p>On this page, the following items are displayed:</p><ul><li>Taxes</li><li>Fees</li><li>Duties  </li><li>Digital River Terms and Conditions </li><li>Payment information</li><li>Product information</li></ul>                                                                                                                                                                                                                                                                                                                                                                      |

{% hint style="info" %}
See [Fulfillment/cancellation flow](../user-guide/fulfillment-cancellation-flow.md) for instructions on how to test this process.
{% endhint %}
