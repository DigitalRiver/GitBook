---
description: >-
  Boleto (meaning 'ticket') Bancário is an official Brazilian payment method,
  which is regulated by the Central Bank of Brazil.
---

# Boleto

{% hint style="warning" %}
Before you can use the Boleto payment method, you must attach a tax ID to the cart.  See [Best practices](../payments-solutions/digitalriver.js/payment-methods/configuring-boleto.md#best-practices) for instructions.
{% endhint %}

Digital River has partnered with PPRO, a payment aggregator, to provide Boleto Bancário. In Brazil, two-thirds of the 200 million population do not have a credit card, Boleto Bancário is highly popular, generating over 50 million transactions a month. Local and regional merchants often offer discounts for Boleto Bancário payments as there is no chargeback risk, and payments are made upfront. After the shopper selects products or services, they go to the client’s Checkout page to select Boleto Bancário. The client site generates the billing details as a print-optimized voucher. The shopper can then pay at a variety of locations with cash or via bank transfer. Once the payment is received, the client ships the purchase order. Boleto Bancário also facilitates online payments via bank transfer or payment card.&#x20;

Boleto Bancário provides the following benefits:&#x20;

* Accounting for around 25% of all online payment transactions, offering Boleto Bancário is a must for doing business in Brazil.&#x20;
* There are literally thousands of ways a shopper can complete their Boleto payment in Brazil: ATMs, bank branches, and online banking, post office, lottery agent, convenience store, or supermarket.&#x20;
* When it comes to online purchases, Boleto Bancário is especially popular for high-ticket items because many consumers still do not feel secure providing their payment details online.&#x20;

For [refunds](../../admin-apis/refunds/managing-a-refund-for-a-delayed-payment-method.md), the shopper who paid for the original transaction will receive the refund amount. The bank account details for the refund must match the shopper's CPF/CNPJ tax ID. The bank account owner must be identical to the bank account owner of the original request.

## How to configure&#x20;

How you configure Bancontact depends on whether you're using [DigitalRiver.js with Elements](../payments-solutions/digitalriver.js/) or[ Drop-in payments](../payments-solutions/drop-in/).&#x20;

| DigitalRiver.js with Elements                                                                     | Drop-in payments                                                                                 |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| [Configuring Boleto](../payments-solutions/digitalriver.js/payment-methods/configuring-boleto.md) | [Drop-in Payments Integration Guide](../payments-solutions/drop-in/drop-in-integration-guide.md) |

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)