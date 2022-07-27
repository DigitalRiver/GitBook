---
description: >-
  Learn more about the payment methods supported by Drop-in Payments and
  DigitalRiver.js
---

# Supported payment methods

The following table lists the supported payment methods in [Drop-in payments](payments-solutions/drop-in/) and [DigitalRiver.js with elements](payments-solutions/digitalriver.js/). All of these payment methods can be used to make one-time purchases. But only some of them support [recurring transactions](sources/#reusable-or-single-use).&#x20;

The table also lists each [payment method's flow](sources/#payment-flow) and indicates whether that payment method is supported in our [test environment](broken-reference).

For a complete list of payment methods that can be paired with [store credit](../consumer-browsing-experience-1/common-use-cases/applying-store-credit.md), refer to [combining primary and secondary sources](sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](sources/using-the-source-identifier.md) page

| Payment method                                                                                                    | Drop-in Payments | DigitalRiver.js with elements | One-off purchases | Recurring payments | Authentication flow |
| ----------------------------------------------------------------------------------------------------------------- | :--------------: | :---------------------------: | :---------------: | :----------------: | :-----------------: |
| [Alipay](supported-payment-methods.md#alipay)                                                                     |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [Apple Pay](supported-payment-methods.md#apple-pay)                                                               |         ✔        |               ✔               |         ✔         |          -         |      `standard`     |
| [Bancontact](supported-payment-methods.md#bancontact)                                                             |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [Boleto](supported-payment-methods.md#boleto)                                                                     |         -        |               -               |         ✔         |          ✔         |      `redirect`     |
| [bPay](supported-payment-methods.md#bpay)                                                                         |         ✔        |               ✔               |         ✔         |          -         |      `receiver`     |
| [Credit Cards](supported-payment-methods.md#credit-cards)                                                         |         ✔        |               ✔               |         ✔         |          ✔         |      `standard`     |
| [Google Pay](supported-payment-methods.md#google-pay)                                                             |         ✔        |               ✔               |         ✔         |          ✔         |      `standard`     |
| [iDEAL](supported-payment-methods.md#ideal)                                                                       |         ✔        |               ✔               |         ✔         |          ✔         |      `standard`     |
| [Klarna](supported-payment-methods.md#klarna)                                                                     |         ✔        |               ✔               |         ✔         |          ✔         |      `redirect`     |
| [Konbini](supported-payment-methods.md#konbini)                                                                   |         ✔        |               ✔               |         ✔         |          -         |      `receiver`     |
| [Online Banking (IBP)](supported-payment-methods.md#online-banking-ibp)                                           |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [Online Banking (Korea Bank Transfer)](supported-payment-methods.md#online-banking-korea-bank-transfer)           |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [PayCo](supported-payment-methods.md#payco)                                                                       |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [PayPal](supported-payment-methods.md#paypal)                                                                     |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [PayPal Billing](supported-payment-methods.md#paypal-billing-agreement)                                           |         ✔        |               ✔               |         ✔         |          ✔         |      `redirect`     |
| [PayPal Credit](supported-payment-methods.md#paypal-credit)                                                       |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [Pay in 3](supported-payment-methods.md#paypal-in-3)                                                              |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [Pay in 4](supported-payment-methods.md#paypal-in-4)                                                              |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [PayPal RatenZahlung (Installment Payment)](supported-payment-methods.md#paypal-ratenzahlung-installment-payment) |         ✔        |               ✔               |         ✔         |          -         |      `redirect`     |
| [SEPA Direct Debit](supported-payment-methods.md#sepa-direct-debit)                                               |         ✔        |               ✔               |         ✔         |          ✔         |      `redirect`     |
| [TreviPay](supported-payment-methods.md#trevipay)                                                                 |         ✔        |               ✔               |         ✔         |          ✔         |      `redirect`     |
| [Wire Transfer](supported-payment-methods.md#wire-transfer)                                                       |         ✔        |               ✔               |         ✔         |          -         |      `receiver`     |

## Alipay&#x20;

Established in 2004, Alipay is China’s leader in third-party online payments and has an estimated 300 million users. Alipay is a delayed fulfillment payment method, meaning fulfillment occurs after authorization and settlement. It works much like PayPal, where the consumer chooses to make a payment and is directed to the external Alipay site, where they enter (or choose existing) payment information.&#x20;

## Apple Pay&#x20;

A fast and secure shopping experience where the consumer can quickly and seamlessly checkout with their Apple Touch authentication without login details or credentials. Digital River will support Apple Pay as a payment method on the payment service and DigitalRiver.js. Apple Pay is currently available to consumers in 21 countries and currently is supported only on IOS devices (iPhones, Macs, and so on).&#x20;

## Bancontact

Bancontact is a Belgian debit card with no chargeback risk (a unique feature for debit cards).&#x20;

## Boleto &#x20;

Boleto (meaning 'ticket') Bancário is an official Brazilian payment method, which is regulated by the Central Bank of Brazil. Digital River has partnered with PPRO, a payment aggregator, to provide Boleto Bancário. In Brazil, two-thirds of the 200 million population do not have a credit card, Boleto Bancário is highly popular, generating over 50 million transactions a month. Local and regional merchants often offer discounts for Boleto Bancário payments as there is no chargeback risk, and payments are made upfront. After the shopper selects products or services, they go to the client’s Checkout page to select Boleto Bancário. The client site generates the billing details as a print-optimized voucher. The shopper can then pay at a variety of locations with cash or via bank transfer. Once the payment is received, the client ships the purchase order. Boleto Bancário also facilitates online payments via bank transfer or payment card. &#x20;

## bPay&#x20;

A wire transfer payment method used in Australia, where users can make payments online and over the phone for online purchases or utility bills. Fulfillment occurs after authorization and settlement. The customer provides either the transfer information to their bank or completes a payment using bPay.&#x20;

## Credit Cards&#x20;

A fast and secure shopping experience where the consumer can purchase goods or services on credit.&#x20;

## Google Pay&#x20;

Allow a merchant to request any credit or debit card stored in their customer’s Google Pay account. This adds another layer of ease-of-purchase for consumers to quickly complete transactions from their Google Wallet. All currencies are available in supported countries.&#x20;

## iDEAL&#x20;

iDEAL allows consumers to authorize payments from their online or mobile banking apps. iDEAL is a bank transfer payment method where the clients receive real-time confirmation of the transaction. It is restricted for use by shoppers who have been issued an online bank account that is iDEAL compatible and held at a bank based in the Netherlands. When using this payment method, a customer must provide their bank with transfer information provided by the merchant to complete the payment. The transfer details consist of the account holder, bank name, city, country description, payment reference, bank account number, additional bank information, and the international bank account number (IBAN).&#x20;

## Klarna&#x20;

Adding Klarna to your store’s checkout offers customers a secure and flexible way to pay for their online purchase over time–while you get paid upfront and without repayment risk. Klarna offers many buy now pay later options including, Pay Later (invoice), Installments, and Financing.&#x20;

## Konbini&#x20;

DSK Konbini is used in Japan and requires a user to complete an order by making a payment at a store using a receipt number or a bank. Konbini is a set of small convenience stores from different brands like Seven Eleven, FamilyMart, Lawson, etc. These stores are very popular in Japan because they are nearly on every corner, so everybody can pay for everything very quickly without the need to have a credit card or other electronic-enabled payment options. Konbini is a delayed fulfillment payment method, meaning fulfillment occurs after authorization and settlement.&#x20;

## Online Banking (IBP)&#x20;

A Browser Redirect processing method, also sometimes called Online Banking, where customers authorize a debit from their bank account. IBP allows customers to use the online banking service provided by their bank.&#x20;

## Online Banking (Korea Bank Transfer)&#x20;

Accept online bank transfers in Korea, a payment method that represents 20% of the local market share. Recurring payments are supported.&#x20;

## PayCo&#x20;

Accept PayCo in Korea, a digital wallet that currently represents a 10% market share and is expected to grow. Recurring payments are supported.&#x20;

## PayPal&#x20;

A digital wallet allowing shoppers to create an account tied to their card or bank account within the PayPal app. Standard PayPal Express Checkout offerings also include Pay Later options (when applicable) so shoppers can place orders, but pay for them over time by leveraging PayPal Credit, PayPal Pay in 3, PayPal Pay in 4, or PayPal RatenZahlung.&#x20;

## PayPal Billing Agreement &#x20;

Consumers can use their PayPal account to make recurring subscription payments. Consumers have the option to choose to auto renew or manually renew.&#x20;

## PayPal Credit&#x20;

Allow consumers to buy online and pay later for their products. This payment method is accepted in thousands of online stores and is available everywhere PayPal is accepted (as long as the PayPal Credit and PayPal accounts are linked). PayPal Credit uses the date of birth and last 4 digits of SSN to approve or deny a consumer for a line of credit, and the applicant will be notified within seconds whether they have been approved or not.

## PayPal in 3&#x20;

PayPal Pay in 3 is a short-term card installment payment option automatically provided by PayPal when a customer signs in to PayPal Checkout. PayPal Pay in 3 allows United Kindom shoppers to pay for physical good purchases in three interest-free monthly payments for purchases between £45 - £2,000 with the first payment due at checkout. Presents within the PayPal wallet on a category known as "Pay Later".&#x20;

## PayPal in 4&#x20;

PayPal Pay in 4 is a pay later option dynamically available through the PayPal Express Checkout Wallet. PayPal Pay in 4 allows shoppers to pay for physical good purchases as follows:

* **France**: four interest-free monthly payments for purchases between €30 to €2,000 with the first payment due at checkout.
* **United States**: four interest-free biweekly payments for purchases between $30 to $600 with the first payment due at checkout.

## PayPal RatenZahlung (Installment Payment)

PayPal RatenZahlung is a pay later option available through PayPal Express Checkout Wallet. Presents within the PayPal wallet on a category known as "Pay Later". Note that PayPal RatenZahlung does not support recurring subscriptions. No additional setup is required to present this payment method in the PayPal Express Checkout Wallet. If the shopper's purchase history along with the items in the checkout qualify, PayPal RatenZahlung will be available as a payment method. &#x20;

## SEPA Direct Debit&#x20;

Allow users to authorize transactions directly from their bank account, which is a popular international payment method.&#x20;

## TreviPay&#x20;

TreviPay allows you to extend a line of credit for business buyers at checkout. This is a fully branded solution facilitating online B2B payments by offering flexible net terms, digital statement handling, collections, credit approval management, and improving the overall B2B online buying experience.&#x20;

## Wire Transfer&#x20;

An offline payment method where a consumer goes to their bank to send the money. When using this payment method, a shopper must provide their bank with transfer information provided by the merchant to complete the payment. The transfer details consist of the account holder, bank name, city, country description, payment reference, bank account number, additional bank information, and the international bank account number (IBAN).
