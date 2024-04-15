---
description: Learn how to export your transactions to CSV or JSON.
---

# Exporting your transactions

## Export as CSV

To export your transactions as CSV:

1. Click **Transactions** in the left navigation. The Transactions page appears.
2. [Filter your transactions](filtering-your-transactions.md), if needed.
3. Click the down arrow ![](<../../../../.gitbook/assets/down-arrow (2).png>) and select **Export as CSV**.\
   ![](<../../../../.gitbook/assets/1 transaction export dropdown csv.png>)
4. Click the **Export as CSV** button (not the arrow).\
   ![](<../../../../.gitbook/assets/2 transaction export csv.png>)\
   The **Save As** dialog appears.
5. Choose a location and file name to save the file.

## Export as JSON

To export your transactions as JSON:

1. Click **Transactions** in the left navigation. The Transactions page appears.
2. [Filter your transactions](filtering-your-transactions.md), if needed.
3. Click the down arrow ![](<../../../../.gitbook/assets/down-arrow (2).png>) and click **Export as JSON**.\
   ![](<../../../../.gitbook/assets/3 transaction export dropdown json.png>)\

4. Click the **Export as JSON** button (not the arrow).\
   ![](<../../../../.gitbook/assets/4 transaction export json.png>)\
   The **Save As** dialog appears.
5. Choose a location and file name to save the file.

{% hint style="info" %}
**Note:** If your application supports the use of metadata, and you want to see it in your transaction data export, we provide metadata support for orders and line items. This metadata is reported in your CSV or JSON export of Transaction information but is NOT visible on the Digital River Dashboard Transactions page.

For CSV exports, your metadata appears in your export file as additional data columns. The metadata columns will use the following labels:

* orderMetadata._your\_key\_value_ – where _your\_key\_value_ is the unique value you assigned to the order metadata. For example, orderMetadata._couponProgram_.
* lineItemMetadata._your\_key\_value_ – where _your\_key\_value_ is the unique value you assigned to the line item metadata. For example, lineItemMetadata._customerID_.
{% endhint %}
