---
description: Learn what custom components are used in the checkout subflows.
---

# Custom components used in the checkout subflows

The Salesforce Lightning application comes with a completely functional checkout flow out-of-the-box (OOTB). However, you can choose to customize your checkout flow to suit your particular needs. This section describes how you can use the Salesforce Lightning components provided by the application in your storefront.&#x20;

| Custom subflow name                                                                     | Custom components used                                                                         | Description                                                                                  |
| --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| [DR Shipping Address](subflow-configuration/configure-the-shipping-address-subflow/)    | drb2b\_buyerInfo                                                                               | This custom subflow will be used in the place of OOTB subflow – Shipping Address.            |
| [DR Delivery Method](subflow-configuration/configure-the-delivery-method-subflow.md)    | drb2b\_drUtil                                                                                  | This custom subflow will be used in the place of OOTB subflow – Delivery Method.             |
| [DR Checkout Summary](subflow-configuration/configure-the-checkout-summary-subflow.md)  | <p>drb2b_drUtil </p><p>drb2b_drTermsElement drb2b_taxIdentifier</p>                            | This custom subflow will be used in the place of OOTB subflow – Checkout Summary.            |
| [DR Payments](subflow-configuration/configure-the-payment-and-billing-address-subflow/) | <p>drb2b_orderSummary </p><p>drb2b_paymentDetails</p><p>drb2b_drUtil </p><p>drb2b_payments</p> | This custom subflow will be used in the place of OOTB subflow – Payment and Billing Address. |

