---
description: Understand how to use BPE.
---

# Bulk Product Export (BPE)

## Bulk Product Export (BPE)

Use the Bulk Product Export (BPE) process to export a catalog for a specific site or company to a file in an XML format. The file is compatible with the BPU process.

{% hint style="info" %}
Note: BPE is non-interactive. When the BPE process finishes, there is no required notification response. When the BPE process ends, an export file indicates the bulk file upload has completed.
{% endhint %}

The BPE process is an inbound event.

### Schemas

<table><thead><tr><th width="148">Version</th><th>Schema Components Table</th><th>Raw Schema</th><th>Sample XML</th></tr></thead><tbody><tr><td>11 (Current)</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/BulkExport/11">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/BulkExport/11">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/BulkExport/11">View</a></td></tr><tr><td>10</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/BulkExport/10">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/BulkExport/10">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/BulkExport/10">View</a></td></tr><tr><td>9</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/BulkExport/9">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/BulkExport/9">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/BulkExport/9">View</a></td></tr></tbody></table>

## Catalog feed

The Catalog Feed API provides a complete record of the products available to a retailer. A batched business process provides the data in XML format over FTP.

### Details

The following steps outline how to implement the business process for the product catalog:

1. The client completes the product profile form (whih is included in the Business Users Guide).
2. Digital River sets up the business process according to this form.
3. The client implements and tests the business process on their side to ensure the business process works.

This business process is available in batch mode only because of the substantial amount of data that is being shared.

The following table shows the business process specifics.

| Characteristic          | Specification |
| ----------------------- | ------------- |
| Business Process Type   | Batch Only    |
| Communication Protocols | FTP Only      |
| Data Formats Available  | XML           |

The business process architecture diagram for the product catalog business process (see image below) shows a combination of several views. It combines a data flow view, an implementation view, and a process flow view into a common, condensed view. This view provides developers with fewer architectural views that make it simpler to understand and implement the Integrated Channel Partner Program (ICPP).

![ICCP System Architecture](https://files.readme.io/730c6ac-Catalog\_feed.png)

The client creates one file each time they run the product catalog extract. Files are in the client’s home directory under the /PRODUCTCATALOG directory on the Digital River FTP server or the client’s FTP servers. Digital River archives files for 30 days.

{% hint style="success" %}
**Best Practices**: Clients should also maintain an archive.
{% endhint %}

The export file contains all the products that are currently available for purchase by a customer. When the client imports the file, the client should scan for products that are in their database but are no longer in their feed. These products are retired and should not be available for sale on the client's site. After the client flags the retired products in their database, they can reimport the entire catalog feed so all updates and changed data elements are available in addition to new products.

Digital River exports the full catalog once per day.

{% hint style="success" %}
**Best Practices**: Clients should import this full catalog every day to keep in sync with changes, receive new products, and retire products that are no longer available.&#x20;
{% endhint %}

### Terminology

| Term                                      | Definition                                                                                                                                                                  |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client                                    | The Digital River business partner who participates in the Integrated Channel Partner Program (ICPP).                                                                       |
| Digital River Product ID                  | The product's ID used internally by the Digital River system.                                                                                                               |
| Integrated Channel Partner Program (ICPP) | The specific product offering provided by Digital River that enables clients the ability to offer the Digital River product catalog to their customers.                     |
| Application Programming Interface (API)   | A set of routines that an application uses to request and carry out lower-level services.                                                                                   |
| Uniform Resource Locator (URL)            | An Internet standard that allows for the precise discovery of websites and other web resources.                                                                             |
| Business process                          | A data trading agreement between two companies. The business process is all-encompassing and includes both the business rules and the technical rules of the data exchange. |
| Extensible Markup Language (XML)          | The data feed Digital River sends to the client, and the order fulfillment requests the client sends to Digital River are in XML format.                                    |

### Schemas

<table><thead><tr><th width="148">Version</th><th>Schema Components Table</th><th>Raw Schema</th><th>XML Schema</th></tr></thead><tbody><tr><td>1 (Current) </td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/IntegratedRetailerChannelExport/1">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/IntegratedRetailerChannelExport/1">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/IntegratedRetailerChannelExport/1">View</a></td></tr></tbody></table>

## Invoice report

The Invoice Report represents the financial-related information used to reconcile orders and returns for billing and/or credit. A batched business process provides the data in XML format over FTP.

### Details

The Invoice response document represents the financial-related information used for the reconciliation of orders and returns for billing and/or credit. Digital River can support other formats such as proprietary CSV, but we highly encourage the use of our XML format. This report is provided weekly to the client and is available via FTP. A separate monthly billing statement will be sent to the client, upon Digital River expecting payment. The client’s bill will be generated monthly in Excel and sent along with the combined CSV files for the month to the client.

The following table shows the business process specifics.

| Characteristic          | Specification |
| ----------------------- | ------------- |
| Business Process Type   | Batch only    |
| Communication Protocols | FTP only      |
| Data Formats Available  | XML           |

Digital River creates one file for the client each the time invoice report extract runs. Files are placed in the client’s home directory under the /REPORTING/INVOICEREPORT/ directory on the Digital River FTP server or the client’s FTP servers. Digital River archives files for 30 days. We recommend that the client also maintains an archive.

The export file contains all placed orders on the client’s site.

Digital River runs the invoice report once per week on Monday mornings at 7 am.

{% hint style="success" %}
**Best Practices**: The client should import this invoice feed for their accounting records.
{% endhint %}

The following image shows an example of a monthly billing statement.

![Monthly billing statement](https://files.readme.io/ed3e4a9-monthly\_billing\_statement.gif)

### Schemas

<table><thead><tr><th width="148">Version</th><th>Schema Components Table</th><th>Raw Schema</th><th>Sample XML</th></tr></thead><tbody><tr><td>1 (Current)</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/IntegratedRetailerInvoiceReport/1">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/IntegratedRetailerInvoiceReport/1">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/IntegratedRetailerInvoiceReport/1">View</a></td></tr></tbody></table>

## Sales reporting

The Sales Reporting runs once a day and always on a 2-3-day lag. It includes all the sales data for a specific site or company over a particular period. When a sale occurs, the system generates a Sales Order Activity and sends it to your endpoint. The Sales Order Activity Info contains the shipping information or returns information for all line items in a single order. &#x20;



The following table describes the contents of a sales notification.

<table><thead><tr><th width="572">Description</th><th width="93.33333333333331">Physical</th><th>Digital</th></tr></thead><tbody><tr><td>Always runs on a 2-3-day lag to account for timings related to fraud and orders transferred from remote databases.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Includes "fulfilled" orders, not necessarily money collected.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Includes delayed payment orders that cleared for that day.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Excludes any suppression (frauded out order) if the suppression occurred within the lag period. Otherwise, the order will be included in the feed.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td><strong>Best Practices</strong>: Use a 3-day lag.</td><td></td><td></td></tr><tr><td>Does not reflect chargebacks or reversals.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td><strong>Cancelled Orders</strong></td><td></td><td></td></tr><tr><td>Digital River cancelled an order because of suppression after running the report, the suppression will not be visible in that report.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Orders or line items of orders cancelled because of a shopper's request or a fulfiller's notification will not be included in the feed.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Orders or line items of orders cancelled because of a fraud suppression may be included in the feed. The orders or orders' line items will be included, and have no indication of the cancellation if the fraud suppression occurred after the fulfiller shipped the items, and after the Sales Notification service generated the fee. The order or orders' line items will not be in the feed at all if the fraud suppression occurred after the fulfiller shipped the items before the Sales Notification service generated the feed.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td><strong>Date Order Appears in the Sales Feed</strong></td><td></td><td></td></tr><tr><td>The date the fulfiller told us the order shipped (usually equivalent to the date when the item shipped).</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td></tr><tr><td>The digital fulfillment date, which is usually within seconds of order submission if the download is hosted by Digital River. If the download is not hosted by Digital River, the date of digital fulfillment (when URL was delivered).</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td> <strong>Returns</strong></td><td></td><td></td></tr><tr><td>The date the product returned to the warehouse.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>If LOD is required, this is the date when the system received the LO. If nothing is required, this is the date when the system created the return.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>If the return completed on the same day, both a (+) and a (-) entry will appear within the same file.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>If the returned product has digital rights (serial numbers or unlock codes), then the serial number or unlock code associated with the return is also provided.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Fees charged to clients are not part of this feed (for example download fees).</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Includes returns as negative values.</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td><p></p><p>Shows satisfaction refunds (CSR returns money to the customer to make them happy, but and the customer keeps the product). The following Satisfaction Return types are available:</p><ul><li>Line Item Level Satisfaction Refund</li><li>Order Level Satisfaction Refund</li><li>Satisfaction Refund (DEPRECATED)</li></ul></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td><p></p><p>Other supported return types include:</p><ul><li>Line Item Level Return Product</li><li>Order Level Return Product</li><li>TaxExemptRefund</li><li>AutoCreateLineItemLevelReturnProduct</li><li>CancelRequestReturnProduct</li><li>ReturnProduct (DEPRECATED)</li></ul></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr></tbody></table>

### Details

The Sales Notification Feed contains many `amount` elements.

A Line Item Satisfaction Refund allows you to refund money to the shopper because the shopper is upset or experienced undue hardship to get the product. The shopper is not required to return any product. See [Line-item level satisfaction refund](line-item-level-satisfaction-refund.md) for an example.

An Order Level Satisfaction Refund allows you to return money to the shopper when a shopper is upset or goes through undue hardship to get the product. The shopper is not required to return any product. See [Order-level satisfaction refund](order-level-satisfaction-refund.md) for an example.

Return receipt arrived with no prior return established. See [Auto-created line-item level return product](auto-created-line-item-level-return-product.md) for an example.

Returned a quantity on a line item, or the entire quantity on the order. See [Line-item level return product](line-item-level-return-product.md) for an example.

### Schemas

<table><thead><tr><th width="143">Version</th><th>Schema Components Table</th><th>Raw Schema</th><th>Sample XML</th></tr></thead><tbody><tr><td>18 (Current)</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/SalesOrderActivityInfoArray/18">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/SalesOrderActivityInfoArray/18">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/SalesOrderActivityInfoArray/18">View</a></td></tr><tr><td>17</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/SalesOrderActivityInfoArray/17">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/SalesOrderActivityInfoArray/17">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/SalesOrderActivityInfoArray/17">View</a></td></tr><tr><td>16</td><td><a href="https://drhadmin.digitalriver.com/integration/isg/schematable/SalesOrderActivityInfoArray/16">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/xsd/SalesOrderActivityInfoArray/16">View</a></td><td><a href="https://drhadmin.digitalriver.com/integration/isg/example/SalesOrderActivityInfoArray/16">View</a></td></tr></tbody></table>

## Reporting

You can use Reporting to see if a report is available for downloading and download the report.

### Checking the availability of a report

The following example shows the Reporting call you must send to get a list of all available reports. The response contains the list of available reports.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```xml
GET https://api.digitalriver.com/reporting/files/all
```
{% endcode %}
{% endtab %}

{% tab title="Response" %}
{% code overflow="wrap" %}
```json
[
  {"filename": "TransactionCustomerDetail.zip","size": "249.333 KB","link": "/lenovo/files/TransactionCustomerDetail.zip","modification_ts": 1540996235000,"modification_date": "2018-10-31"
  }
]
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Downloading the report

The following example shows the Reporting call you need to send to download a specific report, where \<File Name> is the name of the zip file containing the report.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```http
GET https://api.digitalriver.com/reporting/files/<File Name>.zip
```
{% endcode %}
{% endtab %}
{% endtabs %}
