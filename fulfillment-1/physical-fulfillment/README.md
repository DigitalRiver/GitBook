---
description: Learn how to integrate the commerce platform with a new fulfillment source.
---

# Physical fulfillment

Physical fulfillment connects a commerce site to logistics partners who drop-ship products to the shopper. Physical fulfillment also enables a commerce site to smart-source orders through one or more of its partners, in the pre-integrated distribution partner network, who fulfill products globally based on configurable rules. Use this documentation to connect new fulfillment partners and their warehouses with the Digital River ecosystem for order and return management.

| Event                      | Type    |
| -------------------------- | ------- |
| Sales Catalog              | Inbound |
| Inventory Advice           | Inbound |
| Fulfillment Order Request  | Webhook |
| Fulfillment Order Response | Inbound |
| Shipment Notification      | Inbound |
| Return Notification        | Webhook |
| Return Response            | Inbound |
| Return Receipt             | Inbound |

![Physical Fulfillment](https://files.readme.io/79861bb-Physical\_Fulfillment.png)

## Sales catalog

The Sales Catalog integration loads the fulfillment partner’s catalog of products into the Digital River Physical Fulfillment system. This feed typically contains the following data:

* The following table displays the supported formats and data interchange modes from the fulfillment partner to Digital River.
* SKU of the fulfillment partner
* Manufacturer’s part number for the product
* Weight and dimension data of the product

For clients and fulfillers using a Distribution Model, Digital River also requires the unit cost of the product. This detail is included in the unit cost segment. Please note that the unit cost is the amount the fulfiller/distributor is selling the product for to Digital River (that is, not the amount they charge the shopper).

{% tabs %}
{% tab title="XML" %}
{% code overflow="wrap" %}
```xml
<unitCost>
  <c:amount>5.00</c:amount>
  <c:currencyCode>USD</c:curencyCode>
</unitCost>
```
{% endcode %}
{% endtab %}
{% endtabs %}

This feed is not a Site Catalog that provides content and assets to the commerce site hosted at Digital River Global Commerce.

### Supported formats and data interchange modes

| Format        | AS2                       | FTP/SFTP                        | Web Service Post to Digital River |
| ------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML           | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (832) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Full file (Weekly/On-demand)
* Delta daily

### XML specification

* **File name format**: Catalog\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/product.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/product.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/product-import-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/product-import-request.xml)

See the [EDI X12 832 definition data elements](edi-x12-832-definition-data-elements.md) for more information.

## Inventory advice

The Inventory Advice integration imports inventory information from a fulfillment partner's warehouse into the Digital River Physical Fulfillment system.

### Supported formats and data interchange modes

| Format        | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| ------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML           | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (846) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Full file or delta—hourly

### XML specification

* **Filename format**: Inventory\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/inventory.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/inventory.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/inventory-import-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/catalog/inventory-import-request.xml)

See the [EDI X12 846 definition data elements](edi-x12-846-definition-data-elements.md) for more information.

## Fulfillment order request

Digital River sends the purchase order request to the fulfillment partner who will ship the order directly to the customer. The purchase order contains information such as products ordered, quantity ordered, shipping, and shipping address.

### Supported formats

The following table displays the supported formats and data interchange modes from the fulfillment partner to Digital River.

| Format        | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| ------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML           | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (850) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Real-time or Batch at a scheduled interval

### XML specification

* **Filename format**: OrderRequest\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/order.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/order.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-request.xml)

### EDI X12 850 specification

* **Filename format**: OrderRequest\_YYYYMMDD\_HHMISS.xml
* **EDI X12 850 supported version**: 00401

See the [EDI X12 850 definition of data elements](edi-x12-850-definition-data-elements.md) for more information.

## Fulfillment order response

The fulfillment partner sends a response for each order request indicating whether the order was accepted or rejected/cancelled due to errors. If a product is not available, and if the order request allowed the option to hold the backorder by the fulfillment partner, the fulfillment partner uses this feed to notify backorder status. The system sends the purchase order request to the fulfillment partner who will ship the order directly to the customer. The purchase order contains information such as products ordered, quantity ordered, shipping, and shipping address.

### Supported formats

The following table displays the supported formats and data interchange modes from the fulfillment partner to Digital River.

### Recommended frequency

* Real-time or Batch at a scheduled interval

| Format        | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| ------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML           | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (855) | Supported (Best Practice) | Supported                       | Not Supported                     |

### XML specification

* **Filename format**: OrderResponse\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/order.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/order.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-status-notification.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-status-notification.xml)

### EDI X12 855 specification

* **Filename format**: EDI855\_YYYYMMDD\_HHMISS.edi
* **EDI X12 855 supported version**: 00401

See the [EDI X12 855 definition of data elements](edi-x12-855-definition-data-elements.md) for more information.

## Cancel fulfillment order request

Digital River sends the cancel order request to the fulfillment partner so the fulfillment partner can cancel the order at fulfillment. The cancel order contains information such as purchase order number, products cancelled, and quantity cancelled.

### Supported formats and data interchange modes (Digital River to fulfillment partner)

| Format | AS2       | FTP/SFTP                        | Web Service Post to Fulfiller |
| ------ | --------- | ------------------------------- | ----------------------------- |
| XML    | Supported | **Recommended (Best Practice)** | Not Supported                 |

### Recommended frequency

* Batch at a scheduled interval

### XML specification

* **Filename format**: CancelRequest\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel-request.xml)

## Cancel fulfillment order response

The fulfillment partner sends a response for each cancel order request. The response indicates whether the system accepted or rejected the cancellation of the order.

### Supported formats and data interchange modes (fulfillment partner to Digital River)

| Format | AS2       | FTP/SFTP                        | Web Service Post to Fulfiller |
| ------ | --------- | ------------------------------- | ----------------------------- |
| XML    | Supported | **Recommended (Best Practice)** | Not Supported                 |

### Recommended frequency

* Batch at a scheduled interval

### XML specification

* **Filename format**: CancelResponse\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel-status-notification.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/fulfillment-cancel-status-notification.xml)

## Shipment notification

The fulfiller ships the product to the customer and sends a notification to Digital River Global Fulfillment with package details and tracking numbers. Global Fulfillment imports this information and notifies the customer. You can also use this feed to send backorders notifications.

If Digital River has a distribution relationship with the Fulfillment Partner, send the invoice amounts to this feed.

{% hint style="info" %}
**Note**: This information applies only to distribution relationships.
{% endhint %}

In a distribution model where the fulfiller invoices Digital River for the shipping, unit cost (× quantity) and tax, you must call out the following:

#### EDI 856 / shipment notification

* The file must include the `lineItem` segment
* You must include the shipping amount and the subtotal amount in the segment
  * The fulfiller/distributor invoices Digital River for the shipping amount and should be charged to the customer
  * The subtotal amount is the unit cost (same unit cost as noted in the [Sales Catalog](./#sales-catalog)) multiplied by the quantity

{% tabs %}
{% tab title="XML" %}
```markup
<lineItems>
  <lineItem>
  	<rowId>1</rowId>
		<sku>FULFILLE PART NUMBER</sku>
    <warehouseId>AB01</warehouseId>
    <orderQuantity>2</orderQuantity>
    <shippedQuantity>2</shippedQuantity>
    <invoicePricing>
      <c:shipping>
        <c:amount>5.00</c:amount>
        <c:currencyCode>USD</c:currencyCode>
      </c:shipping>
      <c:handling>
        <c:amount>0.00</c:amount>
        <c:curencyCode>USD</c:currencyCode>
      </c:handling>
      <c:tax>
        <c:amount>1.00<c:amount>
        <c:currencyCode>USD</c:currencyCode>
      </c:tax>
      <c:fee>
        <c:amount>0.00</c:amount>
        <c:currencyCode>USD</c:currencyCode>
      </c:fee>
      <c:discount>
        <c:amount>0.0</c:amount>
        <c:currencyCode>USD</c:currencyCode>
      <c:discount>
      <c:subTotal>
        <c:amount>5.00</c:amount>
        <c:currencyCode>USD</c:currencyCode>
      </c:subTotal>
      <c:total>
        <c:amount>11.00</c:amount>
        <c:currencyCode>USD</c:currencyCode>
      </c:total>
    </invoicePricing>
  </lineItem>
</lineItems>     
```
{% endtab %}
{% endtabs %}

### Supported formats

| Format        | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| ------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML           | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (856) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Batch—Daily at scheduled one or more scheduled times

### XML specification

* **Filename format**: Shipment\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/shipment.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/shipment.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/shipment-import-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/shipment-import-request.xml)

### EDI X12 856 specification

* **Filename format**: EDI856\_YYYYMMDD\_HHMISS.edi
* **EDI X12 856 supported version**: 00401

See the [EDI X12 856 definition of data elements](edi-x12-856-definition-data-elements.md) for more information.

## Return notification

If a customer initiates the return of products in an order, Digital River sends the return pre-advice to the fulfillment partner.

### Supported formats

The following table displays the supported formats and data interchange modes from the fulfillment partner to Digital River.

| Format          | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| --------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML             | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (180-1) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Batch at scheduled intervals

### XML specification

* **Filename format**: returnNotification\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-request.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-request.xml)

### EDI X12 180-1 specification

* **Filename format**: EDI180-1\_YYYYMMDD\_HHMISS.edi
* **EDI X12 832 supported version**: 00401

See [EDI X12 180-1 definition of data elements](edi-x12-180-1-definition-data-elements.md) for more information.

## Return response

The fulfillment partner sends a response with warehouse RMA ID and optionally a return warehouse address to Digital River. The response is based on the return notification pre-advice send to the fulfillment partner.

### Supported formats

The following table displays the supported formats and data interchange modes from the fulfillment partner to Digital River.

| Format          | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| --------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML             | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (180-2) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Batch at scheduled intervals

### XML specification

* **Filename format**: returnResponse\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-status-notification.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-status-notification.xml)

### EDI X12 180-2 specification

* **Filename format**: EDI180-2\_YYYYMMDD\_HHMISS.edi
* **EDI X12 180-2 supported version**: 00401

See [EDI X12 180-2 definition of data elements](edi-x12-180-2-definition-of-data-elements.md) for more information.

## Return receipt

When returned packages arrive at the warehouse, the Fulfillment partner notifies Digital River Physical Fulfillment to complete the return with a credit payment. This integration notifies Digital River of any returns without a valid return pre-advice from Digital River. This includes shipments refused by the customer or shipments that the fulfillment partner could not deliver to the customer.

### Supported formats

| Format          | AS2                       | FTP/SFTP                        | Web Service Post to Fulfiller     |
| --------------- | ------------------------- | ------------------------------- | --------------------------------- |
| XML             | Supported                 | **Recommended (Best Practice)** | Supported (Custom Implementation) |
| EDI X12 (180-3) | Supported (Best Practice) | Supported                       | Not Supported                     |

### Recommended frequency

* Batch at scheduled intervals

### XML specification

* **Filename format**: returnReceipt\_YYYYMMDD\_HHMISS.xml
* **XML schema**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return.xsd)
* **XML sample**: [https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-received.xml](https://fulfillment-api.digitalriver.com/v1/fulfiller-account/return-fulfillment-received.xml)

### EDI X12 180-3 specification

* **Filename format**: EDI180-3\_YYYYMMDD\_HHMISS.edi
* **EDI X12 180-3 supported version**: 00401

See [EDI X12 180-3 definition of data elements](edi-x12-180-3-definition-of-data-elements.md) for more information.
