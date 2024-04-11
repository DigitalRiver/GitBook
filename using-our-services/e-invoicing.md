---
description: >-
  Gain a better understanding of Digital River's e-invoicing service and how you
  can use it to collect information from customers in Taiwan
---

# e-Invoicing

You can use Digital River's e-invoicing service to collect information from customers in Taiwan, thereby allowing you to comply with that country's invoicing requirements.

On this page, you'll find:

* [Background information on Taiwan's invoicing system](e-invoicing.md#background)
* [Your integration options](e-invoicing.md#using-the-e-invoicing-service)

## Background

If you'd like to make domestic sales in Taiwan, you must comply with that country's invoicing requirements. Specifically, you must adhere to them when the sale involves [physical goods](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) shipping from and to Taiwan or, in the case of transactions that only involve [digital products](../product-management/skus.md#how-products-are-classified-as-physical-or-digital), billing to that same country.&#x20;

If these conditions are met, Digital River Taiwan acts as the [selling entity](../integration-options/checkouts/creating-checkouts/selling-entities.md), which means specific information must be collected from customers and added to a Government Uniform Invoice (GUI).

{% hint style="info" %}
Contact your Digital River representative to enable the Taiwan selling entity in your account.&#x20;
{% endhint %}

The Taiwanese government uses these invoices to boost revenue and minimize tax avoidance.&#x20;

Companies apply to the government for a series of 8-digit GUI numbers. Every two months, those companies inform the government how many GUI numbers they issued to customers (along with corresponding sales revenue) and how many remain unused. This allows the authorities to get a more accurate picture of whether individual companies engage in tax avoidance.

{% hint style="warning" %}
Taiwan recently introduced electronic GUI mandates to reduce paper waste, which Digital River's e-invoicing service was built to help you comply with.
{% endhint %}

In B2C transactions, customers must designate a media, called a carrier, to associate the GUI number with their identity. Alternatively, they can donate their number to a charity on a pre-approved list.&#x20;

In B2B transactions, customers don't designate a carrier. They must, however, supply their tax identification number for inclusion on the GUI. They can't deduct their business expenses if they fail to do so.&#x20;

After the sale, each GUI number is entered into a government-run lottery. This lottery incentivizes customers to request GUI numbers and only do business with merchants that issue them. Customers holding winning numbers are notified that they've won a cash prize, or their winnings are donated to the charity they selected.

## Using the e-invoicing service

How you interact with the e-invoicing service depends on the checkout solution(s) you've selected. Use the following table to access the appropriate article:

| Checkout solution                                                | Article                                                                                                                       |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [Low-code checkouts](../integration-options/low-code-checkouts/) | [Collecting e-invoice information](../integration-options/low-code-checkouts/collecting-e-invoice-information.md)             |
| [Direct integrations](../integration-options/checkouts/)         | [Handling e-invoicing requirements](../integration-options/checkouts/creating-checkouts/handling-e-invoicing-requirements.md) |

