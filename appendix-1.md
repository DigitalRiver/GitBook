---
description: Learn more about tax codes and view the sequence diagram.
---

# Appendix

## Exhibit A: Eligible tax group, type, and code

[Click this link](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/skus/creating-and-updating-skus#setting-the-tax-code) to learn which tax codes are available in the Digital River API.&#x20;

A Digital River account is required to use this extension. If you do not have a Digital River account, you can sign up for one [here](https://dashboard.digitalriver.com/signup).

## Exhibit B: Sequence diagrams&#x20;

{% file src=".gitbook/assets/Adobe Ext. Sequence Diagram (3).png" %}

{% file src=".gitbook/assets/Adobe Extenstion Sequence Diagram for Refunds.png" %}

## Appendix C: Initiating Refunds

Digital River settles against the payment instrument upon fulfillment of all or part of the order items. Before fulfillment, we collect no funds from the shopper and cannot issue refunds.

Click the Refund Offline button on the Credit Memo page in the Magento Admin UI to issue a refund. When you submit the refund, the system acknowledges it in real-time and, therefore, is not an offline process even though the name of the button is Refund Offline per the Magento convention.

The completion of the refund triggers a webhook. Magento receives the webhook and adds a note regarding the refund in the order’s comment section.

Digital River supports the following Magento refund types: quantity, line level, order level, shipping, tax, adjustment.

{% hint style="info" %}
When you submit an Adjustment Refund for a portion of an order, you should submit all subsequent refunds for that order as Adjustment Refunds.
{% endhint %}
