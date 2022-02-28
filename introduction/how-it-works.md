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

{% file src="../.gitbook/assets/checkout_flow_phase-2.0-latest.png" %}
Download to view the Checkout Flow sequence diagram.
{% endfile %}
