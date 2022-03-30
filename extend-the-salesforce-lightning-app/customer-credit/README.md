---
description: Learn how to enable the customer credit feature.
---

# Customer credit

You can use the [customer credit feature](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/payment-sources/using-the-source-identifier#secondary-payment-sources) to enable several different storefront functionalities such as gift certificates and rewards points.

Salesforce B2B Commerce does not natively support gift cards or store credit functionality. Instead, this functionality is provided by 3rd party integrations. Rather than directly integrating with any of these 3rd parties, the Digital River cartridge provides several functions which make the necessary calls to Digital River to support the customer credit. The System Integrator is responsible for implementing the necessary code changes to call the methods provided by the Digital River app to connect to the 3rd-party integration.

This section describes how the Digital River app supports this feature. It also explains the steps required for you to integrate the customer credit feature based on the use case.

The connector provides the global class, methods, and events in the LWC (Lightning Web Component) to support customer credit. Use the global methods to create, delete and attach customer credit to the checkout. The connector components subscribe to events that other components can publish to trigger actions in the connector components. To integrate this feature with the storefront, call the methods and events as described in this section.

The current version of the Digital River app provides the following global class with global methods that support customer credit.

| **Global Class**   | `DRB2B_CustomerCreditService`                                                                                                                                                                                                                                                                                                                                                   |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Global Methods** | <p><a href="addcustomercreditsourcetocheckout.md"><code>addCustomerCreditSourceToCheckout</code></a><br><a href="deattachpaymenttocheckout.md"><code>deattachPaymentToCheckout</code></a><br><a href="getamountremainingforcheckout.md"><code>getAmountRemainingforCheckout</code></a><br><a href="getcartdetailsbyid.md"><code>getCartDetailsById</code></a><code>​</code></p> |

## Customer credit flow

{% file src="../../.gitbook/assets/SF Lightning - Customer Credit.png" %}