---
description: Learn more about invoices and credit memos.
---

# Invoices and credit memos

## Prerequisites

* An order is placed on a site/location that will generate an invoice.
* PDF invoices are created for all sales made by Digital River Ireland, Ltd.
* PDF invoices are created for all sales made by Digital River, Inc. (except where they are specifically suppressed by the client).
* PDF invoices are created for all sales made by Digital River Global Tech, Inc. (except where they are specifically suppressed by the client).
* Electronic invoices called a Nota Fiscal Eletrônica are created for all sales made by Digital River Brazil.
* Electronic invoices called Electronic Government Uniform Invoices (eGUI) are created for all sales made by Digital River Taiwan.
* A paper invoice called a Fapiao is created upon request for sales made by Digital River China.&#x20;
* A paper invoice is created upon request for sales made by Digital River Korea.&#x20;
* Digital River does not currently generate invoices for sales made by Digital River Japan.

## Invoice and credit memo flow

The Digital River Invoice and Credit Memo file information will be captured in the custom object `DR Invoice And Credit Memo`. When an `order.invoice.created` event is generated for an order, the Salesforce Lightning app consumes this webhook event and stamps the `Invoice File Id` on the custom `File ID` field and `Invoice` on the custom `File Type` field available on custom `DR Invoice` and `Credit Memo` object for the order in question.

Similarly, when an `order.credit_memo.created` event is generated for an order, the app consumes this webhook event and stamps the `Credit Memo File Id` on the custom `File ID` field and `Credit Memo` on the custom `File Type` field available on the custom `DR Invoice and Credit Memo` object for the order in question.&#x20;

## Download the invoice or credit memo file

To download the Invoice and/or Credit Memo for an Order, the customer must follow the steps below:

1. Log in to the storefront. The customer can view their orders by going to **My Account** and then selecting **My Orders**.
2. Go to the **Order Detail/Order Summary** page to open the order for which you need to download the Invoice/Credit Memo.
3. Click the **View Invoice/Credit Memo** link to download the **Invoice/Credit Memo** file.

The **Invoice** and/or **Credit Memo** links are available only on orders for which the Invoice File ID and/or Credit Memo File ID are generated and stamped on the `DR Invoice and Credit Memo` object.

![](<../.gitbook/assets/Invoice and credit memo object.png>)
