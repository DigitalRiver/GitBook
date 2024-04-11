---
description: Understand common terms used throughout the documentation
---

# Glossary

## API key

A token passed by an application calling an API to identify the calling application.

## Authorization

Refers to the verification and validation of credit card information.

## Autorenew

A subscription term that indicates whether a subscription is automatically renewed (and the customer billed) when the subscription period expires.

## B2B

Business to business

## Billing address

The customer's billing address

## Billing term

The time between the start and end of a billing cycle. A one-year subscription paid monthly has twelve billing terms.

## BOGO

Buy One, Get One

## Card verification code

A three- or four-digit code that appears in the signature area on the back of a credit card. They are meant to reduce fraud by ensuring customers physically have the card in their possession.

## Catalog

A catalog is a collection of products organized into categories for a store. Each site implements a catalog of products. A company can have multiple catalogs. A site typically has one catalog. A catalog typically has multiple categories.

## Chargeback

The reversal of payment (i.e., the return of funds) to a customer. Chargebacks occur after payment has been collected. They are different from a return or refund because chargebacks usually occur when customers did not authorize the payment and they contact their payment provider to reverse the payment.

## COD

Cash on delivery

## Cost of goods sold

The total inventory costs of sold goods within a specific timeframe.

## Cross-border

Cross-border refers to selling and shipping [physical products](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) across international borders. In other words, transactions in which goods ship from one country and into another.

However, in the Digital River APIs, certain groups of countries that have formed trade agreements, such as those in the European Union and the Economic Community of West African States, exist as a single political entity. As a result, shipments between them are not considered to be cross-border.

For example, when a transaction involves shipping goods between EU member nations, [tariff codes](glossary.md#tariff-code) aren't required and import taxes and duties aren't collected.

## Currency

The type or format of money used in a particular country or locale.

## Denied parties list (DPL)

A list of people or companies whose purchasing privileges have been denied by Digital River.

## Display currency

The currency used for the price that appears on a storefront.

## ECCN

Export Control Classification Number

## Fulfiller

An entity or company that warehouses and coordinates the shipping of physical products to shoppers who placed an order.

## Fulfillment

The steps involved in receiving, processing, and delivering physical or digital orders to customers.

## Global logistics provider

A global logistics provider (GLP) specializes in shipping physical products across international borders.

They are experts in country-specific regulatory requirements, understand how to prepare shipping documents, and can submit pre-clearance requests to an importation country's customs agency.

They also typically have proprietary international shipping lanes, multiple export gateways, various final mile delivery options, and several logistics models offerings.

For more information, refer to the [Global Logistics](../using-our-services/global-logistics.md) page.

## Headless order management

A new suite of APIs that enable Digital River clients to customize their ecommerce solution. You can connect the commerce platform of your choice with our back-end order management, payments, and risk protection services.

## Importer of record

The importer of record (IOR) is the owner or purchaser of the products being imported into a destination country.

## Landed cost

The total price of a product once it has arrived at the buyer's door. A landed cost includes the original price of the product plus all transportation charges (both inland and ocean), customs, duties, taxes, insurance, currency conversion, packaging, handling, and payment fees.

## Late presentment chargebacks

Late presentment chargebacks occur when a deadline to present a transaction to the issuing bank is missed. These types of chargebacks aren't initiated by the customer. Instead, they originate with the issuing bank.&#x20;

In many cases, the customer doesn't have a problem with the delay, but the issuing bank initiates a chargeback anyways because the transaction is presented to them outside of an allowable time frame.

## Line item

A single line in a cart. At a minimum, a line item contains a single product identifier and quantity.

## Locale

A locale represents a language, country, and currency. A code identifies the locale. For example, the United States English is `en_US`. Locales are not limited to a single country or language. A country can have more than one locale, and some countries share locales. For example, Canada has two locales because it has two official languages: English and French.

## Locale code

A two-letter code that represents a language and country. For example, `en_GB` represents the English language and the country of Great Britain.

## Localization

The process of customizing a store for different nationalities, cultures, languages, and currencies.

## Manufacturer part number

The number the manufacturer uses to identify a product. This value can be localized and set for a variation.

## Merchant of record/seller of record (MOR/SOR)

The Merchant of Record/Seller of Record (MOR/SOR) assumes the risk of the sale, managing taxes and regulations on your behalf.

## Parcel collection point

An alternative delivery location. Parcel collection points are typically stand-alone lockers located in high traffic areas like shopping centers and train stations, or ‘parcel shops’ such as convenience and grocery stores.

## Partial fulfillment

Occurs when a fulfiller ships one or more items within a fulfillment request, but does not ship all of the items in the request. Also known as partial shipment.

## Partial shipment

Occurs when a fulfiller ships one or more items within a fulfillment request, but does not ship all of the items in the request. Also known as partial fulfillment.

## Payment method

The way that a customer chooses to pay for an order (for example, credit card or wire transfer).

## Price list

A list of current prices of items for sale. You can use a price list to set the pricing for products in a catalog.

## Production test environment (PTE)

Digital River’s environment for partners and clients to [test the Digital River APIs](../developer-resources/testing-scenarios.md).

## **Regulatory fees**

Fees set by the government. These fees can be included or added to the product price.

## **Renewal**

Once a subscription period ends, a customer can either manually or automatically renew it.

## Shipping address

The address where the customer wants the order shipped.

## Shipping terms

A shipment's terms can either be delivered-duty-paid (DDP) or delivered-at-place (DAP).&#x20;

In DDP shipments, customers pays all duties, fees, and import taxes upfront, during the checkout process. Upon product delivery, there are no additional charges they must pay.

In DAP shipments, customers do _not_ pay the full [landed cost](../integration-options/checkouts/creating-checkouts/landed-costs.md) at checkout-time. Instead, they pay product and shipping costs, and then, upon delivery, they're responsible for paying duties, fees, and import taxes.

## Stock keeping unit (SKU)

A common product identification scheme.

## Tariff code

A tariff code, also known as a Harmonized System code, is an internationally standardized system used to classify and identify goods.&#x20;

These codes enable customs authorities and merchants to identify the type of goods being imported or exported. They're crucial for determining applicable duties, taxes, and regulations.

The Harmonized System, which covers a wide range of products, including raw materials, intermediate goods, and finished products, is managed by the World Customs Organization.&#x20;

Each code consists of six to ten digits. The first six digits are internationally standardized but individual countries may add extra digits for their specific purposes.

The code classification is hierarchical, meaning that the initial digits represent broader categories of products, while subsequent digits provide more specificity. For example:

* The first two digits represent the chapter, which broadly categorizes goods (e.g., 88 for aircraft and spacecraft).
* The first four digits represent the heading, which provides a more specific classification within the chapter (e.g., 8801 for non-powered aircraft).
* The first six digits represent the subheading, giving even more detail (e.g., 880100 for balloons, dirigibles, gliders, and hang gliders).

Tariff codes are essential for trade documentation as well as customs clearance and misclassifications can potentially result in problems during [cross-border](glossary.md#cross-border) transactions.&#x20;

To learn more about Digital River's tariff code classification service, refer to [Item classification](../using-our-services/item-classification.md).&#x20;

## Terms of sale

The payment and delivery terms agreed to by a buyer and seller.

## Third-party fulfillment agent

An external physical fulfiller.

## **Third-party logistics**

Third-party logistics (3PL) is the outsourcing of a company's distribution, warehousing, and fulfillment requirements to a third-party provider. 3PL providers specialize in delivering these requirements by integrating warehousing and transportation services.

## Transaction

A purchase transaction or requisition that consists of a customer's information and the products they want to purchase.

## Transaction currency

The currency used during the payment of a transaction.

## Universal unique identifier (UUID)

A 128-bit number used to identify some object or entity on the Internet.

## Value-added tax (VAT)

A type of transaction tax placed on a product whenever a value is added at each stage of production and at the final sale. The European Union and other countries worldwide use VAT.

## VAT invoice

The record of sale that must be provided (often within 30 days, and sometimes only on demand) to all customers in a VAT-eligible sale. A complete invoice includes information such as the goods or services in the purchase, the customer’s name and address, the VAT rate, the final VAT paid, the Seller of Title’s name and address, and VAT registration number. Digital River automatically creates a VAT invoice each time a VAT sale occurs, and customers can view or print this invoice as needed.
