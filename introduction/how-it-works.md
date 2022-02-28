# How it works



Use the Salesforce B2B Commerce App to enable Digital River to be the merchant of record for storefronts hosted in Salesforce B2B Commerce.

1. Salesforce B2B Commerce maintains all pricing and product data.
2. Digital River maintains minimal product data used to fulfill its requirements as the merchant of record. This data is used for tax calculations, tax collection, tax payments, and payment processing
3. Digital River automatically syncs with the CC Product in Salesforce B2B Commerce with minimal information needed to calculate taxes and enable the merchant of record functions.
4. Digital River maintains a copy of the cart, customer, and order.

## Checkout flow <a href="#checkout-flow" id="checkout-flow"></a>

The following sequence diagram shows the interaction between the Shopper, Salesforce B2B Commerce, the Salesforce B2B Commerce App, and Digital River.

{% hint style="info" %}
The app currently does not support Guest checkout.
{% endhint %}

{% file src="../.gitbook/assets/sfb2b_checkout_flow-2.1.1.png" %}

## Tax estimations

1. The app extends the global extension point `ccrz.cc_hk_TaxCalculation`.
2. The app creates a Digital River checkout object based on the Salesforce B2B Commerce cart with product information, prices, and quantity. This checkout request is serialized as JSON and posted to a Digital River web service.
3. The response contains the cart tax amount.
