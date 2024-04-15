---
description: Learn how to view the order details.
---

# Viewing the order details

The **Order details** page shows the details of the order. It includes the date ordered, order ID, order email, order [upstream ID](../../../../integration-options/checkouts/creating-checkouts/providing-an-upstream-identifier.md), order status, [SKU ID](../../../../product-management/creating-and-updating-skus.md), product ID ([SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs/operation/listSkus)), product name, part number, status, purchase quantity, item discount, purchase amount, shipping fee, order discount, importer duty, importer tax, [fees](../../../../product-management/regulatory-fees/managing-regulatory-fees.md), tax, order total, metadata at the order level, type of payment, payment details, billing address, payment total, store credit, ship to and ship from addresses, shipping method, tracking information, customer information, tax type, tax ID, tax state, returns and refunds, and shipping timeline.

{% hint style="info" %}
If the order status is <mark style="color:red;">`Disputed`</mark>, some actions cannot be completed until this order is resolved. Digital River Dashboard will disable the Cancel items and Fulfill items links, and the Create return and Create refund buttons. If you try to programmatically [capture or cancel payment](../../../../order-management/informing-digital-river-of-a-fulfillment.md), [issue refunds](../../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md), or [process returns](../../../../order-management/returns-and-refunds-1/returns/) on that order, you will be redirected to the **Order details** page.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/1 nu orders order details.png" alt=""><figcaption></figcaption></figure>

To view the order details:

1. Click **Orders** in the left navigation. The Orders page appears.
2. [Filter your orders](filtering-your-orders.md), if needed.
3. Click the order ID link under the **ID** column. The Order details page appears.
4.  To view fees, [landed cost](../../../../integration-options/checkouts/creating-checkouts/landed-costs.md) (including importer duty and importer tax), discount, tax, and metadata for a line item, expand the row. The summary displays the total fees, discounts, and taxes.\
    \


    <figure><img src="../../../../.gitbook/assets/2 nu order details partial.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** An order item is either identified by a **SKU ID** or **Product ID** - not both. A Product ID is the identifier of the product in the upstream system. This identifier can appear instead of SKU ID if the item uses SKU groups.
{% endhint %}
